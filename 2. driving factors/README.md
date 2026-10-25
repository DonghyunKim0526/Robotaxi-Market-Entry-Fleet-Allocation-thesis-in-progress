# Demand inputs and driving factors

## Demand is scale × choice

```math
D_c=M_cp_c,\qquad M_c=\sum_gN_{c,g}r_g.
```

$M$ counts potential trip opportunities; $p$ is the share choosing robotaxi before fleet shortages. A variable associated with observed trip counts need not identify which of these two components it changes.

| Research step | Main conclusion | Consequence for the model |
|---|---|---|
| Background evidence | Observed robotaxi demand, conventional ride-hailing, and stated-choice studies measure different things | Keep evidence scope and units explicit |
| Candidate screening | Population/activity describe scale; fares, waiting time, access to cars, and attitudes may affect choice | Check whether values are available for every candidate city |
| Final input design | Fix $M$ using population composition × trip rates; estimate $p$ with exogenous context | Avoid estimating both components from the same unseparated trip total |

## Selected direction

- **Market size:** use NHTS group trip rates with ACS group populations; geography, year, trip eligibility, and person/household units must be aligned.
- **Initial exogenous choice variables:** zero-vehicle household share and age composition. The present ER-DRO toy implementation uses only zero-vehicle share.
- **Decision-dependent extension:** own fare, waiting time, and support features require service/choice response data before entering the optimization as endogenous effects.
- **Operational feasibility:** permission and ODD compatibility are separate from user choice probability.

Completed robotaxi trips divided by $M$ measure realized usage and may be censored by supply. Request/rejection data or an explicit adjustment is needed to interpret it as unconstrained choice demand. This folder specifies definitions and selection rules; it does not contain a fitted real-data demand model.

## Related folders

- [A. Background_Research](A.%20Background_Research/README.md)
- [B. Candidates](B.%20Candidates/candidates_%28M%2Cp%29.pdf)
- [C. Selection](C.%20Selection/README.md)
- [※ translation](%E2%80%BB%20translation/README.md)


---

[Parent guide](../README.md) · [Project overview](../README.md)
