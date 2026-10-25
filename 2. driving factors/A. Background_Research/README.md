# Background research

## Three questions addressed by the evidence

| Question | Material | Main takeaway |
|---|---|---|
| Where might a company enter? | Operator/market inventory | Public service, pilots, and announced rollout markets are different statuses |
| What explains demand or choice? | Demand-variable literature review | Only one reviewed paper directly studies observed robotaxi demand; conventional ride-hailing and stated preferences supply indirect evidence |
| Can service operate there? | City-entry conditions review | ODD compatibility and legal/operating permission are feasibility conditions; weather and infrastructure can be risk descriptors |

## Main papers and how they are used

The [Research guide](1%29%20Research/README.md) maps individual papers to their roles; the [demand-variable review](1%29%20Research/02_demand_variables.pdf) contains the detailed evidence and source links.

| Main reference | Contribution | Use in the project |
|---|---|---|
| **Loa, Lee & Circella — Just another ride-hailing?** | Observed SF robotaxi trip associations, including zero-vehicle households | Supports the current ER-DRO context and candidate-variable rationale; the reported slope informs a synthetic coefficient, not a calibrated cross-city choice model |
| **Elkhouly & Alhadidi — Ride-sharing Determinants** | Conventional ride-hailing associations with population, activity, income, and car availability | Screens M/p candidates and measurable city characteristics; indirect robotaxi evidence |
| **Zhang et al. — Examining spatial heterogeneity of ridesourcing demand determinants** | Built-environment/accessibility variables with nonlinear and spatially varying effects | Informs urban-form candidates and cautions against a universal coefficient sign |
| **Cats et al. — Beyond the dichotomy** | Substitution/complementarity between ride-hailing and public transport | Informs alternative-service competitiveness and the interpretation of transit variables |
| **Yin & Cherchi — Willingness to pay for automated taxis** | Choice trade-offs involving fares, waits, support features, and reviews | Supports service-variable screening and a planned decision-dependent extension; these effects are not yet implemented in the current model |
| **Wei et al. — Extended UTAUT study of robotaxi acceptance** | Survey-based acceptance, value, and habit mechanisms | Informs candidate interpretation and data needs; latent scores are not directly used as city context, and the study does not measure trust |
| **Yin, Cherchi & Nettle — Living in a City Where Automated Taxis are Operating and Using Them** | Operating-area exposure and individual experience in preferences | Informs experience/awareness candidates without assuming a uniformly positive experience effect |

Five additional SAV/AV references in the review cover pilot-based adoption, SAV/AV preferences, a stated-choice review, and pilot-user/ridership evaluation. They broaden the demographic, attitudinal, service, and experience evidence but do not all supply implemented regressors or direct robotaxi-demand estimates.

**Connection to the current work:** [Candidates](../B.%20Candidates/candidates_%28M%2Cp%29.pdf) collects the evidence-backed pool; [Selection](../C.%20Selection/README.md) defines fixed M and uncertain p and screens measurable variables; [ER-DRO](../../1.%20model/C.%20ER-DRO_model/README.md) currently uses zero-vehicle household share as its sole context in the synthetic experiment. Age and service variables remain selection/extension directions, not completed real-data estimates.

## Implication for $D=Mp$

Population and trip generation help construct market scale $M$. Choice attributes and city characteristics can explain $p$, but a relationship with total observed trips does not separate $M$ from $p$. Public ACS/SLD/GTFS measurements make variables comparable; measurement availability alone is not evidence of a demand effect.

The current working review is in `1) Research`; the dated demand-review snapshot is kept separately. Operator-market lists are document snapshots and should be checked against their linked sources before selecting real operating areas.

## Related folders

- [1) Research](1%29%20Research/README.md)


---

[Parent guide](../README.md) · [Project overview](../../README.md)
