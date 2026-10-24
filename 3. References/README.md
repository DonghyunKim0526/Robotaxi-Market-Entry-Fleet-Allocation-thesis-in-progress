# References and parameter rationale

## Why these references matter

| Material | Key conclusion for this project |
|---|---|
| Cost-component rationale | Entry, vehicle cost, and lost contribution have structural literature support; an extra unused-capacity penalty is a study assumption |
| Baseline parameter rationale | Reported observations, published estimates, derived scale values, and synthetic assumptions are different evidence levels |
| Multi-source papers | Trust and source bias can be modeled explicitly instead of pooling all sources as equally reliable |
| DRO papers | Reweighting known scenarios and transporting outcomes lead to different ambiguity sets |
| Contextual optimization papers | Regression plus residuals supplies city-conditional scenarios; decision dependence requires a further model |

## Parameter anchors used in annual experiments

| Parameter | Experimental baseline | Interpretation |
|---|---:|---|
| $\kappa$ | 8,760 trips/vehicle-year | 24 trips/day ×365; derived scale assumption, not observed maximum capacity |
| Reference $M$ | 770,544,140 opportunities/year | Reported TNC count / 5% mode share; source scopes do not perfectly match |
| $F$ | USD 3.5M | Facility project scale plus assumed preparation allowance |
| $K$ | USD 7,972/vehicle-year | Personal-vehicle ownership-cost components used as a proxy |
| $c^+,c^-$ | 0 and 10 USD/trip | Extra idle penalty absent; unmet loss uses a contribution-margin reference |

The parameter PDF and implemented annual notebook use different exploratory $p$ levels; the experiment README records the actual scenario inputs. Korean and English parameter PDFs also retain different probability ranges. These scale references do not make the synthetic case a real-city calibration.

## The methodological bridge

$$
\text{city context }x\ \longrightarrow\ \hat f(x)+\text{residual scenarios}
\ \longrightarrow\ \min_a\sup_{P\in\mathcal U(x)}\mathbb E_P[c(a,D)].
$$

C3 supplies residual SAA, C4 extends residual learning to DRO, and the EV-location paper shows what changes when demand also depends on decisions. The present robotaxi notebook implements exogenous-context CVaR ER-DRO, not all mechanisms covered in the reference collection.

## Documents and their contents

- **[A. cost_selection_rationale.pdf](A.%20cost_selection_rationale.pdf)** — Maps entry/fleet/unmet-loss components to literature and identifies extra idle penalties as a study assumption; structural support is separate from coefficient calibration.
- **[B. parameter_rationale_baseline.pdf](B.%20parameter_rationale_baseline.pdf)** — Tracks O/E/D/A evidence labels and derives annual capacity, market scale, entry/fleet-cost proxies, and synthetic sensitivity levels.


## Related folders

- [※ papers](%E2%80%BB%20papers/README.md)
- [※ translation](%E2%80%BB%20translation/README.md)


---

[Parent guide](../README.md) · [Project overview](../README.md)
