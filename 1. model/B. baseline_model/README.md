# Baseline model

| Folder | What it contains |
|---|---|
| [1) baseline](1%29%20baseline/README.md) | Mathematical formulation, demand/cost definitions, and the meaning of entry, fleet, surplus, and shortage variables |
| [2) numerical_experiments](2%29%20numerical_experiments/README.md) | Small and annual synthetic experiments: independent implementation checks, boundary tests, sensitivity, and uncertainty comparisons, with reports and executable notebooks |
| [3) revision_history](3%29%20revision_history/README.md) | Retained earlier formulations and a change log explaining what changed, the supported reasons, and editorial cleanup |

## What the baseline models

Before observing demand, an operator selects candidate cities and allocates an integer fleet. City demand is fixed market size times a specified scenario choice probability, $D_c^s=M_cp_c^s$. The same entry/fleet decisions apply to every scenario; surplus capacity and unmet demand are then calculated city by city.

```math
\min_{y,q,O,U}\sum_cF_cy_c+\sum_cK_cq_c+
\frac1{|S|}\sum_{s,c}(c_c^+O_c^s+c_c^-U_c^s)
```

Here $y_c$ is binary entry, $q_c$ is vehicles, $F_c$ is entry cost, and $K_c$ is annual vehicle cost. Capacity is $\kappa_cq_c$; $O_c^s$ and $U_c^s$ measure unused capacity and unmet robotaxi demand. City limits $q_c\le\bar q_cy_c$, total fleet $\sum_cq_c\le Q$, and capacity balance $\kappa_cq_c-D_c^s=O_c^s-U_c^s$ connect deployment to service outcomes. The objective balances fixed expansion costs against expected surplus/shortage losses. See [the formulation](1%29%20baseline/baseline%28main%29.pdf) for full notation and constraints.

## Numerical experiments: purpose and design

The experiments establish whether this formulation is implemented correctly and whether its behavior can be explained by its costs, constraints, and demand assumptions. Final fleet vectors are reference outputs rather than the main research conclusion.

| Question | Small case | Annual large case |
|---|---|---|
| Why this setting? | Simple synthetic integers make the model inspectable and directly enumerable | Literature-informed scale proxies test annual-scale behavior; probability levels place demand near capacity |
| Core settings | 3 cities, 10 fixed equiprobable scenarios; $M=(80,100,120)$, $Q=4$, city cap 2, productivity 10 | 3 cities, 10 equiprobable scenarios; city market sizes at 0.75/1/1.25 of the reference, $Q=1,000$, city cap 500, productivity 8,760 |
| Independent verification | Enumerate all 60 feasible entry/fleet pairs; check balance, limits, domains, and objective | Exact dynamic programming plus feasibility/objective recomputation and small reference checks |
| Behavior examined | Eight boundary cases; entry-cost switching, productivity, city demand scale, idle penalty, and mean-preserving dispersion | Eight scale-appropriate boundary cases; common/city-specific sensitivity, tied optima, and scenario resampling |
| Uncertainty comparison | Evaluate all tied mean-demand decisions under the original scenarios | The same common-distribution comparison, plus 50/100/500 samples with five seeds each |

Small-case values are designed for verification, not estimated from actual cities. Annual inputs combine public scale references, arithmetic derivations, and explicit assumptions; they are not a calibrated city-demand model. Each case guide explains its inputs and evidence limits.

### What the model checks reveal

- **Implementation:** the reported MILP results agree with the independent references in the tested instances. Boundary cases distinguish no service incentive, prohibitive entry cost, exact demand/capacity balance, and resource constraints.
- **Entry economics:** extra service is not automatically worth entering another city. In the small case, the third city's extra contribution is 8 against entry cost 20; changing common entry cost produces an interpretable switch at $F=8$.
- **Capacity and cost mechanisms:** increasing total fleet helps only while city caps and demand allow it. Performance can change without a fleet-vector change; common and city-specific cost changes can have different effects.
- **Uncertainty and ties:** the same mean demand can hide different scenario-specific shortages and idle capacity. A representative allocation alone can hide changes in the full optimal set; the annual baseline has 72 tied allocations.

![Small-case entry-cost sensitivity: allocation, service, cost components, and improvement over no entry.](2%29%20numerical_experiments/small_case/figures/smallcase/06_F_zoom.png)

**Economic interpretation:** the small-case switch can be traced to additional service contribution versus fixed entry cost. The figure checks that the optimizer responds for a reason consistent with the objective, rather than merely displaying a final deployment.

![Annual scenario-sampling stability: sampled mean demand and extra decision cost under the common original distribution.](2%29%20numerical_experiments/large_case/figures/annual/17_sampling.png)

**Sampling interpretation:** at 50 scenarios, seed-dependent decisions can cost up to about USD 1.73M more when evaluated on the original distribution; at 500, all five tested seeds have zero extra cost. This is stability under an assumed discrete distribution, not validation against actual robotaxi demand. Fleet shading in sensitivity plots denotes tied-optimum ranges, not confidence intervals.

For reproduction, the small reference fleet is $(0,2,2)$ at cost 858; the annual representative is $(132,368,500)$ at about USD 166.264M. Detailed outcomes, sensitivity mechanisms, and qualifications belong in the case guides below.

### Reports and executable code

| Case | Detailed design and conclusions | Code | Colab |
|---|---|---|---|
| Small | [Guide](2%29%20numerical_experiments/small_case/README.md) · [Report](2%29%20numerical_experiments/small_case/small_case.pdf) | [Notebook](2%29%20numerical_experiments/small_case/baseline_smallcase.ipynb) | [Run](https://colab.research.google.com/drive/1xJvXZokBwrCa2vabDtKB1izIU3fAevtx) |
| Annual large | [Guide](2%29%20numerical_experiments/large_case/README.md) · [Report](2%29%20numerical_experiments/large_case/large_case.pdf) | [Notebook](2%29%20numerical_experiments/large_case/baseline_largecase.ipynb) | [Run](https://colab.research.google.com/drive/1eLKtC6O0tr65SM1JkziHM24RaPbEDo3_) |

Run cells in order to inspect inputs, reference/feasibility checks, boundary tests, and sensitivity/uncertainty results. Colab opens the Drive originals; GitHub notebooks are saved snapshots and do not automatically synchronize.

## Limits and the move to ER-DRO

The baseline takes choice scenarios as given: it does not learn demand from city characteristics or protect against misspecified scenario weights. Its synthetic checks establish implementation behavior, not real-market predictive validity. [C. ER-DRO_model](../C.%20ER-DRO_model/README.md) therefore learns logit choice probabilities and empirical residual scenarios from context, then uses CVaR reweighting to study the expected-cost/tail-risk trade-off. That current extension still assumes exogenous demand; decision-dependent demand and real-data validation remain further work.

[Models overview](../README.md) · [Project overview](../../README.md)
