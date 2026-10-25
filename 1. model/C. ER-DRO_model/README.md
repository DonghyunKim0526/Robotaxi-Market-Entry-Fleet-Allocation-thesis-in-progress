# ER-DRO model and experiments

## Two-stage ER-DRO model

Following [ER-DRO(revised).pdf](ER-DRO%28revised%29.pdf), the model chooses city entry and fleet allocation before demand is known. It minimizes entry cost plus CVaR of the scenario-dependent surplus/shortage cost. Demand is exogenous to these decisions in this version.

### Stage 1: city entry and fleet allocation

```math
\begin{aligned}
\min_{y,q}\quad &\sum_{c\in C}F_cy_c+\mathcal R_\zeta(q)\\
\text{s.t.}\quad &0\le q_c\le\bar q_cy_c &&\forall c\in C,\\
&\sum_{c\in C}q_c\le Q,\\
&y_c\in\{0,1\},\quad q_c\in\mathbb Z_{\ge0} &&\forall c\in C.
\end{aligned}
```

$y_c$ selects a city and $q_c$ allocates vehicles; both are shared across scenarios. $F_c$ is entry cost, $\bar q_c$ is the city fleet cap, and $Q$ is total available fleet. The risk term is

```math
\mathcal R_\zeta(q)=\min_{\tau\in\mathbb R}
\left\{\tau+\frac1{N(1-\zeta)}\sum_{s=1}^N[H(q,D^s)-\tau]_+\right\},
\qquad 0\le\zeta<1.
```

### Stage 2: surplus capacity and unmet demand

For fixed fleet $q$ and scenario demand $D^s$, the recourse problem is

```math
\begin{aligned}
H(q,D^s)=\min_{O^s,U^s}\quad
&\sum_{c\in C}(c_c^+O_c^s+c_c^-U_c^s)\\
\text{s.t.}\quad
&\kappa_cq_c-D_c^s=O_c^s-U_c^s &&\forall c\in C,\\
&O_c^s,U_c^s\ge0 &&\forall c\in C.
\end{aligned}
```

$\kappa_c$ is service capacity per vehicle, while $c_c^+$ and $c_c^-$ price unused capacity and unmet demand. Recourse separates by scenario and city: $O_c^s=(\kappa_cq_c-D_c^s)_+$ and $U_c^s=(D_c^s-\kappa_cq_c)_+$. Vehicles are not reallocated across cities after observing demand. The extensive-form MILP linearizes the risk term using $w^s\ge H(q,D^s)-\tau$, $w^s\ge0$, and embeds each scenario's recourse constraints.

### Contextual demand scenarios

```math
\hat\varepsilon^k=\ln\left(\frac{p^k}{1-p^k}\right)-\hat\beta_0-\hat\beta_1x^k,
\qquad
p_c^s=\sigma(\hat\beta_0+\hat\beta_1x_c+\hat\varepsilon^s),
\qquad D_c^s=M_cp_c^s,
\qquad \sigma(z)=\frac1{1+e^{-z}}.
```

Fit the logit-scale regression from observations $(x^k,p^k)$, then attach each empirical residual to the candidate city's context $x_c$. Market size $M_c$ is fixed, and one residual defines one joint scenario, so the training sample size equals the scenario count $N$. All demand scenarios are computed before optimization.

The revised model omits a separate vehicle-cost term $K_cq_c$; its cost-coefficient interpretation is discussed in the revised document and the version notes below.

## What this model adds

Compared with the baseline's specified choice scenarios, ER-DRO **learns context-dependent demand through logit regression and empirical residuals**, then **reweights the fixed scenarios through a CVaR-type ambiguity set**. At $\zeta=0$ it reduces to ER-SAA; larger $\zeta$ emphasizes high-cost outcomes. It supports studying the value of context and the expected-cost/tail-risk trade-off, while retaining decision-independent demand.

## Experiment design

- **Context:** actual ACS zero-vehicle household shares for 18 candidate-city county proxies. Household totals ×10 supply toy $M$ values.
- **Synthetic learning:** $\beta_0=-3.5$, $\beta_1=0.8$, normal logit error with standard deviation 0.3; train with $N=15,200$.
- **Decisions:** city cap 150, capacity 8,760 trips/vehicle-year, fleet set to about 60% of expected demand (267 vehicles in the reported case).
- **Comparisons:** contextual ER-SAA, contextual ER-DRO, no-context benchmark, and a city-count-budget variant.
- **Evaluation:** 1,000 separate true-model scenarios; report mean cost and the mean of the worst 10% (OOS CVaR at 0.9).

## Solution method comparison: extensive form vs. L-shaped decomposition

The revised document compares two ways of solving the same two-stage model at $N=15$, $c^-=5$, and $\zeta=0.9$:

- **Extensive form:** put first-stage decisions and every scenario's recourse/CVaR constraints into one MILP and solve it with HiGHS.
- **L-shaped decomposition:** iterate between a master problem in $(y,q,\tau)$ and scenario subproblems that evaluate recourse and generate cuts. The stages are linked through these cuts; they are not solved independently once in sequence. Lower/upper bounds determine when to stop.

| Setting | Extensive-form objective / time | L-shaped feasible cost / time | Difference |
|---|---|---|---|
| Entry cost in objective; no city-count budget | 17,304,198 / 1.5 s | 17,378,353 / 54.5 s; 38 iterations | +0.43% |
| City-count limit $B=3$; entry cost removed from objective | 16,036,515 / 0.4 s | 16,140,861 / 29.5 s; 38 iterations | +0.65% |

**Interpretation.** L-shaped stops when the bound gap is within **1% of the upper bound**. Its reported feasible cost can therefore exceed the extensive-form result, and the chosen cities need not be identical. Compare methods within each row: the budget variant changes the objective, so the two rows are not a like-for-like policy-cost comparison.

The extensive form is faster in these toy instances: the surplus/shortage recourse is piecewise linear and can be represented compactly in one MILP. The budget variant reduces decomposition time in the reported run, but does not reduce its 38 iterations. **Subsequent numerical experiments use the extensive form.** This does not establish that it will remain faster for larger or decision-dependent models. Set `RUN_COMPARE=True` in the notebook to reproduce the optional comparison; times are those reported in [ER-DRO(revised).pdf](ER-DRO%28revised%29.pdf), not a new runtime benchmark.

## Main result: expected cost versus tail protection

| $N=200,c^+=1,c^-=5$ | $\zeta=0$ | $\zeta=0.5$ | $\zeta=0.9$ |
|---|---:|---:|---:|
| OOS mean cost (million normalized cost units) | 12.46 | 12.67 | 14.22 |
| OOS tail cost (million normalized cost units) | 22.79 | 22.29 | 21.62 |
| Cities entered | 6 | 5 | 3 |

![OOS mean and worst-10% cost versus risk parameter, with c+=1 and c-=5; larger risk aversion trades average cost for tail protection.](figures/toy_oos_vs_zeta.png)

OOS mean and worst-10% cost versus risk parameter, with c+=1 and c-=5; larger risk aversion trades average cost for tail protection.

Greater conservatism lowers tail cost here while raising average cost. Context improves the no-context comparison, but DRO does not guarantee improvement in every OOS metric: with $N=15$, no-context tail cost can worsen as $\zeta$ increases. The experiment uses synthetic choices, not observed robotaxi demand.

## Learning and solution checks

![Logit fit and residual diagnostics for N=15 and N=200; inspect signal strength and whether residual reuse is plausible.](figures/fig1_f_diagnostics.png)

Logit fit and residual diagnostics for N=15 and N=200; inspect signal strength and whether residual reuse is plausible.

With $N=200$, estimated slope 0.665 and residual standard deviation 0.298 are near the toy truth 0.8 and 0.3. Test $R^2\approx0.143$ reflects weak explanatory signal; residual plots are diagnostic evidence, not proof of independence in real data.

The optional L-shaped comparison stops at 1% relative tolerance. Reported feasible costs are 0.43–0.65% above the extensive form, so it is not an exact-solution equality check. The extensive form was faster for these toy instances.

## Code, outputs, and document versions

Run the notebook top to bottom in Colab. It uses NumPy, SciPy/HiGHS, Matplotlib, and pandas in the diagnostic/export cells. The setup installs SciPy and Matplotlib; pandas is available in the usual Colab environment. `RUN_COMPARE=True` enables the optional decomposition comparison. Later sensitivity cells solve roughly 130 models and take longer than the base loop.

Outputs include `table2_main_results.csv`, `table3_budget.csv`, `table4_sensitivity.csv`, regression diagnostics, OOS-vs-risk plots, and sensitivity plots. Fit diagnostics, decisions, and OOS costs should all be inspected; an in-sample objective alone does not measure generalization.

Read **revised** for the two-stage formulation and logit residuals. **Draft** retains a separate $K_cq_c$ term and earlier residual notation. The revised version omits separate vehicle cost; its coefficient-absorption identity is exact for expectation under the stated adjustment but only approximate for general CVaR ($\zeta>0$), as its derivation notes. Do not treat the revised cost scale as identical to the baseline.

## Documents and their contents

- **[ER-DRO(draft1).pdf](ER-DRO%28draft1%29.pdf)** — Earlier CVaR formulation retaining separate vehicle cost and pre-revision residual notation; compare with revised before using equations.
- **[ER-DRO(revised).pdf](ER-DRO%28revised%29.pdf)** — Two-stage CVaR MILP, logit residual scenarios, toy-data training/OOS design, solution comparison, and risk/sensitivity results.


## Code and Colab launch

- **[ER-DRO(non decision-dependent).ipynb](ER-DRO%28non%20decision-dependent%29.ipynb)** · [Colab](https://colab.research.google.com/drive/1dz5QtiAnYBBmKfDLi95xfjFirqg2fcAT) — Logit learning → residual scenarios → ER-SAA/ER-DRO/no-context decisions → independent OOS scoring; diagnostics, optional decomposition, and CSV exports.

Colab opens the permission-controlled Drive original. The GitHub notebook is a saved snapshot; changes are not automatically synchronized.

---

[Parent guide](../README.md) · [Project overview](../../README.md)
