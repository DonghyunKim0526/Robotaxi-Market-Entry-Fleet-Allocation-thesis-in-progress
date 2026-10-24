# Distributionally robust optimization

## Ambiguity-set choices

```math
\min_a\sup_{P\in\mathcal U}\mathbb E_P[c(a,D)].
```

| Paper | Key idea | What to take from it |
|---|---|---|
| Unifying DRO via optimal transport | A generalized OT construction with conditional moment constraints jointly perturbs likelihood ratios and outcomes | Clarifies how divergence and Wasserstein approaches relate; they model different kinds of misspecification |
| Distributionally robust optimization (survey) | Systematic treatment of ambiguity sets, duality, reformulations, statistical foundations, and regularization links | Reference for choosing a set and stating assumptions behind guarantees |
| Wasserstein DRO with heterogeneous sources | Intersects OT neighborhoods around biased empirical sources; prior bias information can improve OOS performance | A multi-source extension requiring source-specific bias/radius information |

## Relation to the implemented CVaR model

The robotaxi experiment keeps residual-generated scenario locations fixed and changes admissible probability weights:

```math
\mathcal U_\zeta=\{\pi\ge0:\sum_s\pi_s=1,\ \pi_s\le1/[N(1-\zeta)]\}.
```

This produces the CVaR threshold formulation. It is not a Wasserstein ball that moves demand outcomes. Larger $\zeta$ permits more weight on costly existing scenarios; it cannot invent a missing demand scenario. The cited theory and applications do not themselves establish calibrated radii or OOS guarantees for this toy model.

## Documents and their contents

- **[01_Unifying_Distributionally_Robust_Optimization_via_Optimal_Transport_Theory2308.05414v2.pdf](01_Unifying_Distributionally_Robust_Optimization_via_Optimal_Transport_Theory2308.05414v2.pdf)** — Generalized optimal transport links likelihood-ratio ambiguity and outcome perturbations, with duality and tractable reformulations.
- **[02_distributionally-robust-optimization.pdf](02_distributionally-robust-optimization.pdf)** — Broad DRO survey covering ambiguity-set modeling, reformulations, statistical foundations, and links to regularization/adversarial learning.
- **[03_Wasserstein_Distributionally_Robust_Optimization_with_Heterogeneous_Data_Sources2407.13582v1.pdf](03_Wasserstein_Distributionally_Robust_Optimization_with_Heterogeneous_Data_Sources2407.13582v1.pdf)** — Intersects OT neighborhoods around biased sources; studies how source-bias information affects OOS decisions and tractability.


---

[Parent guide](../README.md) · [Project overview](../../../README.md)
