# Baseline model

## Model and economic interpretation

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

- **First stage:** select cities $y_c$ and allocate vehicles $q_c$ once for the evaluation year.
- **Demand:** fixed market size $M_c$ times exogenous robotaxi choice probability $p_c^s$. The scenario probability is $1/|S|$, which is different from $p_c^s$.
- **Cost:** initial entry $F_cy_c$, annual fleet $K_cq_c$, extra unused-capacity penalty, and foregone contribution from unserved trips.
- **Constraints:** no vehicles without entry, city fleet caps, total fleet cap, and demand-capacity balance. Unentered-city demand remains unmet demand.

## What the experiments show

| Instance | Independent check | Representative result | Interpretation |
|---|---|---|---|
| Small: 3 cities, 10 scenarios, $Q=4$ | Enumerate all 60 feasible $(y,q)$ pairs | $(0,2,2)$, objective 858 | Serving 0.8 extra trips in a third city earns 8 but costs 20 to enter |
| Annual: 3 cities, 10 scenarios, $Q=1,000$ | Exact integer dynamic program | $(132,368,500)$, objective 166.264M | Equal marginal values leave 72 optimal B/C fleet splits |

Read the formulation for the model, the numerical-experiment folders for plots and executable checks, and revision history for earlier definitions. Inputs are synthetic; literature references establish scale, not calibrated city demand.

## Related folders

- [1) baseline](1%29%20baseline/README.md)
- [2) numerical_experiments](2%29%20numerical_experiments/README.md)
- [3) revision_history](3%29%20revision_history/README.md)


---

[Parent guide](../README.md) · [Project overview](../../README.md)
