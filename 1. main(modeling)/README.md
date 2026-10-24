# Models and experiments

## Decision structure

All models choose cities and integer fleets before demand is realized. Scenario recourse records surplus service capacity and unmet robotaxi demand; vehicles are not transferred between cities after observing a scenario.

| Model family | Demand construction | Objective and contribution |
|---|---|---|
| Earlier formulations | Exogenous demand scenarios | Compares basic overage/underage, cost, profit, and multiple-penalty formulations |
| Baseline | $D_c^s=M_cp_c^s$ with fixed $M$ and specified $p$ | Entry + annual fleet cost + expected surplus/shortage costs; independently verified experiments |
| Revised ER-DRO | Logit regression + empirical residuals at each city's context | Entry + CVaR of recourse costs; evaluates value of context and tail protection |

## Core baseline formulation

$$
\min_{y,q,O,U}\;\sum_c F_cy_c+\sum_c K_cq_c+
\frac{1}{|S|}\sum_{s,c}(c_c^+O_c^s+c_c^-U_c^s)
$$

$$
D_c^s=M_cp_c^s,\qquad
\kappa_cq_c-D_c^s=O_c^s-U_c^s
$$

$$
0\le q_c\le\bar q_cy_c,\quad \sum_cq_c\le Q,\quad
y_c\in\{0,1\},\ q_c\in\mathbb Z_{\ge0},\ O_c^s,U_c^s\ge0.
$$

$y_c$ is entry, $q_c$ is vehicles, $\kappa_cq_c$ is capacity, and $O,U$ are surplus and shortage in trip units. The fleet limit $Q$ is an upper bound, not a requirement to deploy every vehicle.

## Numerical evidence

- **Small case:** $(0,2,2)$, objective 858, service rate 30%; the extra service from a third city does not pay its entry cost.
- **Annual case:** $(132,368,500)$ is representative of 72 optima; identical marginal values in B and C explain the ties.
- **ER-DRO:** with $N=200,c^-=5$, increasing $\zeta$ from 0 to 0.9 raises OOS mean cost from 12.46M to 14.22M while reducing tail cost from 22.79M to 21.62M in the reported toy experiment.

These are synthetic results. The revised ER-DRO cost normalization differs from the baseline, and Korean companions include some earlier notation; read the current English formulation alongside them.

## Related folders

- [A. former_model ideas](A.%20former_model%20ideas/README.md)
- [B. baseline_model](B.%20baseline_model/README.md)
- [C. ER-DRO_model](C.%20ER-DRO_model/README.md)
- [translation](translation/README.md)


---

[Parent guide](../README.md) · [Project overview](../README.md)
