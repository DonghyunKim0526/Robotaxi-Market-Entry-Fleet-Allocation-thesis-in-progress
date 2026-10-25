# Models and numerical experiments

The current model is **empirical-residuals-based distributionally robust optimization (ER-DRO)** for robotaxi city entry and fleet allocation. It learns choice probabilities from city context, converts fitted residuals into joint demand scenarios, and evaluates deployment decisions against costly demand outcomes.

This overview follows [ER-DRO(revised).pdf](C.%20ER-DRO_model/ER-DRO%28revised%29.pdf), particularly its two-stage formulation, synthetic numerical experiments, and proposed real-data application. Earlier models and baseline implementation checks remain in their own folders.

## Model development and baseline experiments

The research progressed from alternative deployment formulations to an independently checked baseline, then to contextual ER-DRO. The baseline experiments establish implementation correctness and explain entry/capacity economics; the current ER-DRO experiments examine learning, the value of context, and risk protection.

| Stage | Core idea and what was learned | Documents and code |
|---|---|---|
| Earlier model ideas | Compared newsvendor, cost-minimization, profit-maximization, and multiple-penalty formulations; clarified served demand, surplus/shortage, and possible cost double counting | [Former models](A.%20former_model%20ideas/former_models.pdf) |
| Baseline model | Fixed market size and externally specified choice scenarios; minimizes entry + annual vehicle cost + expected surplus/shortage loss, subject to city/total fleet limits | [Formulation](B.%20baseline_model/1%29%20baseline/baseline%28main%29.pdf) |
| Small-case baseline experiment | Three cities and ten joint scenarios; independent enumeration of all 60 feasible entry/fleet pairs verifies the MILP. Edge tests and sensitivity isolate when extra service justifies another city's entry cost | [Report](B.%20baseline_model/2%29%20numerical_experiments/small_case/small_case.pdf) · [Notebook](B.%20baseline_model/2%29%20numerical_experiments/small_case/baseline_smallcase.ipynb) · [Colab](https://colab.research.google.com/drive/1xJvXZokBwrCa2vabDtKB1izIU3fAevtx) |
| Annual baseline experiment | Literature-informed synthetic annual inputs; exact dynamic programming verifies the MILP. Sensitivity and repeated scenario samples explain tied allocations, capacity bottlenecks, and the cost of mean-demand decisions | [Report](B.%20baseline_model/2%29%20numerical_experiments/large_case/large_case.pdf) · [Notebook](B.%20baseline_model/2%29%20numerical_experiments/large_case/baseline_largecase.ipynb) · [Colab](https://colab.research.google.com/drive/1eLKtC6O0tr65SM1JkziHM24RaPbEDo3_) |
| Current ER-DRO | Learns choice probabilities and residual scenarios from city context; compares expected and tail costs under independent evaluation, then tests sensitivity to signal, noise, resources, and sample size | [Revised model and experiments](C.%20ER-DRO_model/ER-DRO%28revised%29.pdf) · [Notebook](C.%20ER-DRO_model/ER-DRO%28non%20decision-dependent%29.ipynb) · [Colab](https://colab.research.google.com/drive/1dz5QtiAnYBBmKfDLi95xfjFirqg2fcAT) |

Colab links open the Drive originals; the GitHub notebooks are saved snapshots. The following sections focus on the latest ER-DRO formulation and its experimental questions.

## Current model: contextual, two-stage ER-DRO

### Demand learning and residual scenarios

Market size $M_c$ is fixed. Uncertainty is in the robotaxi choice probability $p_c$, explained by exogenous context $x_c$ (currently the zero-vehicle household share). Given training observations $(x^k,p^k)$, estimate a linear regression on the logit scale:

```math
\ln\!\left(\frac{p^k}{1-p^k}\right)=\beta_0+\beta_1x^k+\varepsilon^k,
\qquad \hat\varepsilon^k=\ln\!\left(\frac{p^k}{1-p^k}\right)-\hat\beta_0-\hat\beta_1x^k.
```

Attach each fitted residual to a candidate city's context and transform it back into a probability:

```math
p_c^s=\sigma(\hat\beta_0+\hat\beta_1x_c+\hat\varepsilon^s),\qquad
D_c^s=M_cp_c^s,\qquad \sigma(z)=\frac{1}{1+e^{-z}}.
```

One residual defines one joint scenario across candidate cities, so the scenario count equals the training sample size, $|S|=N$. The sigmoid keeps probabilities in $(0,1)$. Demand scenarios are computed **before** optimization: context is exogenous, and demand does not yet respond to fleet or entry decisions.

### Stage 1: entry and fleet allocation before demand is observed

The first-stage decisions are city entry $y_c$ and integer fleet $q_c$. They are chosen once and apply to every demand scenario. The first-stage problem in the revised document is

```math
\begin{aligned}
\min_{y,q}\quad &\sum_{c\in C}F_cy_c+\mathcal R_\zeta(q)\\
\text{s.t.}\quad &0\le q_c\le\bar q_cy_c &&\forall c\in C,\\
&\sum_{c\in C}q_c\le Q,\\
&y_c\in\{0,1\},\quad q_c\in\mathbb Z_{\ge0} &&\forall c\in C.
\end{aligned}
```

$F_c$ is entry cost, $\bar q_c$ is the city fleet cap, and $Q$ is total available fleet. The scenario costs are aggregated by the document's CVaR term:

```math
\mathcal R_\zeta(q)=\min_{\tau\in\mathbb R}
\left\{\tau+\frac{1}{|S|(1-\zeta)}\sum_{s\in S}
\big(H(q,D^s)-\tau\big)^+\right\},\qquad 0\le\zeta<1.
```

At $\zeta=0$ this reduces to the empirical average (ER-SAA); larger $\zeta$ emphasizes high-cost scenarios. The first-stage objective uses the second-stage cost function defined below, rather than choosing a separate fleet for each scenario.

### Stage 2: scenario-specific surplus and unmet demand

With the first-stage fleet $q$ fixed and scenario demand $D^s$ given, solve the recourse problem:

```math
\begin{aligned}
H(q,D^s)=\min_{O^s,U^s}\quad
&\sum_{c\in C}(c_c^+O_c^s+c_c^-U_c^s)\\
\text{s.t.}\quad
&\kappa_cq_c-D_c^s=O_c^s-U_c^s &&\forall c\in C,\\
&O_c^s,U_c^s\ge0 &&\forall c\in C.
\end{aligned}
```

$\kappa_c$ is service capacity per vehicle, while $c_c^+$ and $c_c^-$ price unused capacity and unmet demand. Recourse separates by scenario and city; there is no post-demand transfer of vehicles across cities. The outcome formulas use the revised document's positive-part notation:

```math
O_c^s=\big(\kappa_cq_c-D_c^s\big)^+,\qquad
U_c^s=\big(D_c^s-\kappa_cq_c\big)^+.
```

The superscript plus means the positive part, i.e. the larger of the expression and zero.

### Extensive form: solving the two stages together

The implemented MILP embeds the stage-1 constraints and each scenario's stage-2 constraints in a single problem. It replaces the positive part in the CVaR expression with the revised document's auxiliary variables:

```math
\min_{y,q,O,U,\tau,w}\quad
\sum_{c\in C}F_cy_c+\tau+
\frac{1}{|S|(1-\zeta)}\sum_{s\in S}w^s,
```

```math
w^s\ge\sum_{c\in C}(c_c^+O_c^s+c_c^-U_c^s)-\tau,\qquad
w^s\ge0,\quad\tau\in\mathbb R.
```

Here $y,q$ are the common first-stage decisions; $O^s,U^s$ are scenario-specific second-stage variables; $\tau,w^s$ represent CVaR in the extensive form. The stages describe when decisions/outcomes arise, not a requirement to solve two independent problems sequentially. A variant replaces entry cost in the objective with an entry-budget or city-count constraint.

The revised formulation omits a separate vehicle-cost term $K_cq_c$. Section 1.6 explains the coefficient adjustment: its identity is exact for the expectation formulation, while the analogous absorption inside general CVaR is an approximation. Thus the revised cost specification should not be treated as automatically equivalent to the earlier baseline for every risk level.

## Numerical experiment: what is being tested?

The synthetic experiment tests whether the **estimation–scenario-generation–optimization pipeline works**, what context adds to decisions, how DRO changes the mean/tail trade-off, and how these findings depend on data availability and parameter assumptions. Knowing the true generating model makes these questions measurable through independent evaluation.

### Settings and comparison design

| Component | Setting and purpose |
|---|---|
| Candidate context | 18 candidate-city county proxies; actual ACS 2019–2023 B08201 zero-vehicle household shares, about 0.054–0.777 |
| Market scale | Actual household totals ×10; the multiplier is a synthetic assumption |
| True choice model | $p=\sigma(-3.5+0.8x+\varepsilon)$, with normal error of standard deviation 0.3 |
| Training | Synthetic $(x,p)$ observations, $N=15$ or 200; estimate coefficients and residuals without supplying the true coefficients to the optimizer |
| Capacity and fleet | $\kappa=8,760$ trips/vehicle-year; city cap 150; $Q$ set to about 60% of expected demand divided by productivity (267 vehicles in the reported case) |
| Costs | $c^+=1$, $c^-\in\{1,5,10\}$, $F_c=F_0c^-$ with $F_0=100,000$; scaling entry cost preserves its ratio to unmet-demand loss |
| Risk levels | $\zeta\in\{0,0.5,0.9\}$; 0 is ER-SAA |
| Benchmarks | Contextual ER-SAA; contextual ER-DRO; no-context model under the same comparison settings |
| Independent evaluation | 1,000 separate scenarios from the true demand model, held common across compared decisions |
| Performance measures | OOS expected total cost and OOS tail cost (mean of the worst 10%); regression diagnostics on a separate 1,000-observation test set |

The full sequence is: generate training data → fit logit regression → reuse empirical residuals at candidate contexts → solve the MILP → score the fixed decision on independent true-model scenarios. In-sample optimized costs are not the main evidence of decision quality. The evaluation tail level stays at 0.9 even when the optimization risk parameter $\zeta$ changes.

### 1. Does demand learning recover the intended signal?

![Logit fit, residual distribution, residual-versus-context plots, and prediction diagnostics for N=15 and N=200.](C.%20ER-DRO_model/figures/fig1_f_diagnostics.png)

**Finding.** With $N=200$, the estimated context slope is 0.665 versus the true 0.8, and residual standard deviation is 0.298 versus 0.3. Test $R^2$ is about 0.143, compared with −0.013 for the no-context predictor. The generating model deliberately has a weak contextual signal, so low predictive $R^2$ does not by itself mean context has no decision value.

**Interpretation.** The residual plots check whether reuse across contexts is plausible in this synthetic setting. They do not prove residual independence or cross-city transfer for real observations. Those assumptions need separate validation before applying the model to actual demand.

### 2. What does context add, and what does DRO change?

![Out-of-sample mean cost and worst-10% cost versus the optimization risk parameter; contextual and no-context models with N=15 and N=200, c+=1 and c-=5.](C.%20ER-DRO_model/figures/toy_oos_vs_zeta.png)

| Contextual model, $N=200,c^-=5$ | $\zeta=0$ | $\zeta=0.5$ | $\zeta=0.9$ |
|---|---:|---:|---:|
| OOS expected cost (million normalized cost units) | 12.46 | 12.67 | 14.22 |
| OOS worst-10% cost (same units) | 22.79 | 22.29 | 21.62 |

**Effect of DRO.** From $\zeta=0$ to 0.9, expected cost rises by about 14%, while tail cost falls by about 5.1%. The result illustrates the cost of tail protection; lower expected cost is not the criterion ER-DRO is designed to improve unconditionally.

**Effect of context.** Across the reported $N$ and cost-ratio settings, the contextual model's expected-cost reduction relative to its no-context counterpart is about 1–3% at $\zeta=0$, 3–15% at 0.5, and 4–19% at 0.9. This is a matched-risk comparison, distinct from comparing ER-SAA with ER-DRO.

**Limited-data qualification.** For $N=15$, the no-context model's tail cost can increase as risk aversion grows (22.79M →23.20M at $c^-=5$). Robustifying a poorly informed small residual sample does not guarantee better OOS tail performance. At $\zeta=0.9$, contextual decisions trained with 15 versus 200 observations differ in OOS expected cost by approximately 0.8–3.1% across the tested cost ratios; this is evidence for these synthetic runs, not a general small-sample guarantee.

### 3. Sensitivity: when do the comparisons matter most?

![One-parameter sensitivity analysis: entry cost, fleet availability, city cap, productivity, unmet-demand loss, context strength, noise, training sample size, and risk level.](C.%20ER-DRO_model/figures/fig2_sensitivity.png)

Each panel changes one parameter from $N=200,c^+=1,c^-=5,\zeta=0.9$, holding the other settings fixed. The three lines compare contextual ER-DRO, contextual ER-SAA, and no-context ER-DRO; the figure reports **OOS expected cost**, so the ER-SAA line can be lower while ER-DRO provides tail protection in the preceding comparison.

| Parameter / question | Reported behavior | What can be learned |
|---|---|---|
| Entry cost $F_0$ | ER-DRO expected cost rises about 12.04M →18.73M across tested levels | Entry-cost assumptions materially affect the evaluated policy cost |
| Fleet $Q$ and productivity $\kappa$ | Increasing either reduces expected cost; changing the fleet ratio 0.2→1.0 lowers ER-DRO cost about 16.79M →11.45M | Resource scarcity can dominate learning: at the 0.2 fleet ratio, model costs nearly coincide because capacity is used wherever allocated |
| City cap $\bar q$ | Results plateau above about 100 for ER-SAA and 150 for ER-DRO in the tested instance | Relaxing a nonbinding cap brings no further improvement |
| Context strength $\beta_1$ | The compared costs coincide at zero signal; reported context gains reach about 25% and 41% at slopes 3 and 5 | Context has more decision value when it actually explains demand; the baseline slope 0.8 yields smaller gains |
| Demand noise $\sigma_\varepsilon$ | Higher dispersion raises evaluated expected cost | Demand uncertainty changes the cost scale and the value of checking tail performance |
| Training size $N$ | Over tested $N=10$–200, contextual ER-SAA costs vary within about 1.4%; contextual ER-DRO fluctuates about 13.19M–14.24M | More observations need not produce a monotone improvement in one synthetic realization |
| Unmet-demand loss $c^-$ and risk $\zeta$ | Cost levels and risk preferences change; the reported context comparisons persist across ratios 1:1, 1:5, and 1:10 | The main finding is not tied to a single assumed surplus/shortage ratio; this does not empirically calibrate that ratio |

Changing $\beta_1$ changes the true demand model, so training and estimation are repeated in that sweep. The displayed curves summarize tested parameter settings, not universal monotonicity or statistical confidence bounds.

### Computational check

The revised document also compares the extensive form with L-shaped decomposition at a 1% stopping tolerance. The decomposition's feasible costs are about 0.43–0.65% above the extensive-form results, and it takes longer in these small instances. Subsequent experiments therefore use the extensive form. This comparison checks the solution approach; it does not establish that decomposition is faster or that both methods returned identical exact optima.

## What remains for real-data application

The revised document proposes learning from **operating-city tracts** and aggregating demand over candidate-city tracts:

```math
p_{cj}^s=\sigma(\hat\beta_0+\hat\beta_1x_{cj}+\hat\varepsilon^s),\qquad
D_c^s=\sum_{j\in J_c}M_{cj}p_{cj}^s.
```

Trip counts and potential opportunities must use matching geography and periods. ACS/NHTS would construct tract-level $M$ and context, while operator trip records would provide observed choice shares. The proposed SF→LA validation checks predictive error and residual transfer before applying the relationship to new cities. Data access, supply-censoring effects, residual pooling, and training-range overlap remain to be checked. This is a **planned application**, separate from the completed synthetic experiment.

## Documents and code

- **[ER-DRO revised formulation and experiments](C.%20ER-DRO_model/ER-DRO%28revised%29.pdf):** source for this overview's equations, experiment settings, results, and real-data plan.
- **[English ER-DRO notebook](C.%20ER-DRO_model/ER-DRO%28non%20decision-dependent%29.ipynb) · [Run in Colab](https://colab.research.google.com/drive/1dz5QtiAnYBBmKfDLi95xfjFirqg2fcAT):** run top to bottom for regression diagnostics, residual scenarios, benchmark/OOS comparisons, and sensitivity plots/tables. Optional `RUN_COMPARE=True` enables the decomposition comparison. Colab opens the Drive original; the GitHub file is a saved snapshot.
- **[Baseline model and verification experiments](B.%20baseline_model/README.md):** earlier expected-cost model and independent small/annual implementation checks.
- **[Earlier model ideas](A.%20former_model%20ideas/README.md):** development of alternative cost/profit and penalty formulations.
- **[Korean companion materials](%E2%80%BB%20translation/README.md):** translated model explanations and notebooks.

[Project overview](../README.md)
