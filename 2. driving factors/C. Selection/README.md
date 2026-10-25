# Selected demand inputs

## Selection criteria and screening process

The sequence is **literature-backed candidates → common criteria → candidate-by-candidate screening → preliminary role assignment → data/fitted-model checks**. The detailed decisions are documented in [Factors_of_M.pdf](Factors_of_M.pdf) and [Factors_of_p.pdf](Factors_of_p.pdf).

| Criterion | How it filters candidates |
|---|---|
| Consistent target and evidence | Align trip definitions, geography, period, and the denominator of p; distinguish observed robotaxi use, conventional ride-hailing, and stated preferences |
| Comparable measurement before the decision | Require the same source/definition for every candidate city; defer attitudes or awareness without common survey data |
| Interpretability and parsimony | Avoid overlapping indicators, check correlations, and keep variable count small relative to independent observations |
| Scale versus choice | Keep population/market scale in M; use shares, densities, or relative service conditions for p |
| Model role | Separate exogenous city traits, decision-dependent service attributes, and operating feasibility; being endogenous is a role assignment, not automatic rejection |
| Transfer and residual validity | Check training-range overlap, cross-city transfer, and residual patterns after data collection/fitting; decision-dependent effects also require response data |

### How the criteria led to the current direction

- **M — choose a construction method:** economic activity, income, and zero-vehicle share were considered for a regression of trip rates, but can also explain p. The document instead adopts fixed market scale from population composition × NHTS trip rates to clarify the scale/choice distinction. Geography, eligible trips, sparse groups, and local validation still need data checks.
- **p — prioritize measurable city traits:** zero-vehicle household share and age composition are initial exogenous priorities. Income/activity, density, and other urban indicators are deferred where effects, redundancy, aggregation, or transfer need clarification. Age's city-level effect still needs validation; no uniform sign is imposed.
- **p — retain service effects for an extension:** relative own fare, waiting time, and support features are selected as decision-dependent candidates, pending matched service/choice response data. Survey attitudes, knowledge, and experience are deferred where comparable measurements or interpretation are unresolved.
- **Treat operating conditions separately:** permission and ODD/service availability determine feasibility rather than being interchangeable with a user-choice predictor. In the M screening, annual time/weather effects and ambiguous transit effects were not retained as core scale regressors.

These are preliminary screening decisions, not completed statistical selection. The current synthetic ER-DRO implementation uses **only zero-vehicle household share**; gathering comparable observations and validating the fitted model are later steps.

## Fixed market scale: $M$

```math
M_c=\sum_{g\in G}N_{c,g}r_g
=\mathrm{Population}_c\sum_g\pi_{c,g}r_g.
```

Group $g$ describes population composition, for example vehicle availability × income. $r_g$ is a weighted annual trips-per-person rate from NHTS; $N_{c,g}$ is the city population in that group from ACS. This fixes a comparable $M$ for each city without using the same city covariates to separately regress both $M$ and $p$.

National group rates are transferred to cities. Sparse cells, PUMA-to-city aggregation, household-to-person conversion, eligible-trip definitions, and survey-year alignment must be checked. The document gives a procedure and illustrative numbers; actual-data calculation is not yet completed. Local MPO trip totals provide a validation target.

## Choice probability: $p$

```math
p_c^{\mathrm{obs}}=\frac{\text{robotaxi trips in city }c}{M_c}.
```

| Selected role | Initial variables | Required data |
|---|---|---|
| Exogenous | Zero-vehicle household share; age composition (initially 18–34 share) | ACS B08201 and B01001; comparable city geography |
| Decision-dependent extension | Own relative fare; waiting time; in-vehicle support features | Choices and service outcomes linked to operational changes |
| Separate feasibility | Permission and ODD/service availability | Operating and technical conditions |

The screening above assigns preliminary roles; fitting and cross-city/residual checks are needed before finalizing the predictors.

Completed trips reflect supply constraints. Treating the above observed ratio as pre-shortage choice demand requires request/rejection adjustment or a stated assumption that censoring is small. The current ER-DRO toy uses only zero-vehicle share; selected extension variables are not already implemented.

## Documents and their contents

- **[Factors_of_M.pdf](Factors_of_M.pdf)** — Compares approaches, then specifies fixed M from NHTS group trip rates × ACS group populations, with units, geography, and validation checks.
- **[Factors_of_p.pdf](Factors_of_p.pdf)** — Screens choice variables; prioritizes zero-vehicle share and age, labels fare/wait/features for decision dependence, and states supply-censoring limitations.


---

[Parent guide](../README.md) · [Project overview](../../README.md)
