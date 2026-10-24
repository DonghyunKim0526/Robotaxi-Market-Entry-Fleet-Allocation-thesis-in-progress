# Supporting papers

## What each paper cluster contributes

| Cluster | Central question | Contribution to the robotaxi model |
|---|---|---|
| Multi-source data | How should conflicting sources with uncertain reliability be combined? | Trust-aware ambiguity sets; a possible later alternative to a single empirical residual sample |
| DRO | Which distributions should be protected against? | Likelihood reweighting, outcome transport, and tractable reformulations |
| Contextual optimization | How should decisions change with observed city features? | Conditional prediction, residual scenarios, ER-SAA/ER-DRO, and decision-dependent learning |
| Related applications | How do location and service decisions interact under uncertainty? | Fixed opening decisions, allocation, demand coverage, and operational feasibility |

## Reading logic

Start with C1/C2 for method families, C3 for residual-based SAA, and C4 for robustification with limited data. Then read the EV-location paper for decision-dependent demand. Consult the DRO survey for ambiguity-set definitions and the multi-source papers when source reliability becomes part of the model.

$$
\min_a\mathbb E[c(a,D)\mid X=x]
\quad\longrightarrow\quad
\min_a\sup_{P\in\mathcal U(x)}\mathbb E_P[c(a,D)].
$$

Conditioning on $x$ and protecting against ambiguity are distinct steps. None of these papers alone validates the robotaxi cost coefficients or city demand inputs. This folder holds supporting literature, not additional project experiments.

## Related folders

- [A. multi_sourced_data](A.%20multi_sourced_data/README.md)
- [B. distributionally_robust_optimization](B.%20distributionally_robust_optimization/README.md)
- [C. contextual_stochastic_optimization](C.%20contextual_stochastic_optimization/README.md)
- [D. other_related_papers](D.%20other_related_papers/README.md)


---

[Parent guide](../README.md) · [Project overview](../../README.md)
