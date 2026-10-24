# Baseline formulation

## Objective and constraints

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

| Quantity | Meaning |
|---|---|
| $y_c,q_c$ | Binary entry and nonnegative integer fleet; common to every scenario |
| $M_c,p_c^s,D_c^s$ | Potential all-mode trip opportunities, robotaxi choice probability before shortages, and implied demand |
| $\kappa_c,\bar q_c,Q$ | Trips per vehicle-year, city fleet cap, and total available fleet |
| $O_c^s,U_c^s$ | Unused trip capacity and unmet robotaxi demand in scenario $s$ |
| $F_c,K_c,c_c^+,c_c^-$ | Entry cost, annual vehicle cost, and per-trip surplus/shortage coefficients |

## What the equations imply

For a fixed allocation, operational outcomes can be recomputed as

$$
O_c^s=(\kappa_cq_c-D_c^s)_+,\quad
U_c^s=(D_c^s-\kappa_cq_c)_+,\quad
T_c^s=\min(D_c^s,\kappa_cq_c).
$$

- Capacity cannot move across cities, so unused capacity and unmet demand can coexist in the system.
- Non-robotaxi demand $M_c(1-p_c^s)$ is distinct from robotaxi demand that goes unserved; only the latter enters $U$.
- $c^-$ is lost contribution per trip, not gross fare. A positive $c^+$ is an extra preference penalty and needs justification beyond costs already in $K$.
- Entry cost is paid once; vehicle cost, demand, and capacity cover the same operating year. The objective includes opportunity losses and is not simply cash expenditure.

## Verification result

The companion small experiment produces $(0,2,2)$ at cost 858, matching independent enumeration. The annual experiment uses the same mathematical structure with scaled inputs and an exact dynamic-programming reference. This folder contains the formulation, not an executable notebook.

## Documents and their contents

- **[baseline(main).pdf](baseline%28main%29.pdf)** — Defines demand and cost terms, entry/fleet decisions, capacity balance, and the interpretation of unmet demand; use the current English version to match the implementation.


---

[Parent guide](../README.md) · [Project overview](../../../README.md)
