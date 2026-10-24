# Selected demand inputs

## Fixed market scale: $M$

$$
M_c=\sum_{g\in G}N_{c,g}r_g
=\mathrm{Population}_c\sum_g\pi_{c,g}r_g.
$$

Group $g$ describes population composition, for example vehicle availability × income. $r_g$ is a weighted annual trips-per-person rate from NHTS; $N_{c,g}$ is the city population in that group from ACS. This fixes a comparable $M$ for each city without using the same city covariates to separately regress both $M$ and $p$.

National group rates are transferred to cities. Sparse cells, PUMA-to-city aggregation, household-to-person conversion, eligible-trip definitions, and survey-year alignment must be checked. The document gives a procedure and illustrative numbers; actual-data calculation is not yet completed. Local MPO trip totals provide a validation target.

## Choice probability: $p$

$$p_c^{\mathrm{obs}}=\frac{\text{robotaxi trips in city }c}{M_c}.$$

| Selected role | Initial variables | Required data |
|---|---|---|
| Exogenous | Zero-vehicle household share; age composition (initially 18–34 share) | ACS B08201 and B01001; comparable city geography |
| Decision-dependent extension | Own relative fare; waiting time; in-vehicle support features | Choices and service outcomes linked to operational changes |
| Separate feasibility | Permission and ODD/service availability | Operating and technical conditions |

Selection criteria require interpretable evidence, consistent measurement for all candidate cities, a small nonredundant variable set, and support overlap with training data. After fitting, inspect residual patterns and transfer across cities. Selection is preliminary, not proof of predictive performance.

Completed trips reflect supply constraints. Treating the above observed ratio as pre-shortage choice demand requires request/rejection adjustment or a stated assumption that censoring is small. The current ER-DRO toy uses only zero-vehicle share; selected extension variables are not already implemented.

## Documents and their contents

- **[Factors_of_M.pdf](Factors_of_M.pdf)** — Compares approaches, then specifies fixed M from NHTS group trip rates × ACS group populations, with units, geography, and validation checks.
- **[Factors_of_p.pdf](Factors_of_p.pdf)** — Screens choice variables; prioritizes zero-vehicle share and age, labels fare/wait/features for decision dependence, and states supply-censoring limitations.


---

[Parent guide](../README.md) · [Project overview](../../README.md)
