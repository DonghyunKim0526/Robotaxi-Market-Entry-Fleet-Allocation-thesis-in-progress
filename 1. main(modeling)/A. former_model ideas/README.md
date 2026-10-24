# Earlier model formulations

## Formulations compared

| Formulation | Objective logic | What it adds |
|---|---|---|
| Basic newsvendor | Expected unused capacity + weighted unmet demand | A deployment benchmark before monetary calibration |
| Cost model | Entry + fleet cost + scenario penalties | Makes the cost of entering another city explicit |
| Profit model | Served-trip contribution less entry/fleet costs | Connects service to revenue and incremental operating cost |
| Multiple penalties | Separate surplus and unmet-demand consequences | Distinguishes different losses after capacity is exhausted |

$$
R_c^s=\min(D_c^s,\kappa_cq_c),\quad
O_c^s=(\kappa_cq_c-D_c^s)_+,\quad U_c^s=(D_c^s-\kappa_cq_c)_+.
$$

The common decisions are binary entry $y_c$ and integer fleet $q_c$. This earlier document additionally discusses feasibility $y_c\le a_c$, a city-count limit $\sum_cy_c\le B$, and a minimum one vehicle when a city is entered. Those restrictions are not all part of the current baseline.

**Modeling lesson:** do not count lost trip contribution twice through both a profit term and an unmet-demand penalty. Surplus, shortage, and served trips are calculated from demand and capacity; they are not separate datasets to estimate.

This folder records the progression of ideas, rather than a numerical experiment or the current specification.

## Documents and their contents

- **[former_models.pdf](former_models.pdf)** — Compares newsvendor, cost, profit, and multiple-penalty formulations; defines served demand, surplus, shortage, entry feasibility, and fleet constraints.


---

[Parent guide](../README.md) · [Project overview](../../README.md)
