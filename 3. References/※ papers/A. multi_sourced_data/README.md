# Multi-source data and information fusion

## Source reliability and information fusion

| Paper | Main method / result | Relevance and boundary |
|---|---|---|
| Multi-sourced information with unknown reliability | Multi-reference Wasserstein DRO, nonparametric fusion, dynamic trust updates, and probability dominance; LP reformulation for a linear setting | Models trust across conflicting sources; not implemented in the present single-residual-sample robotaxi notebook |
| Trust-aided parametric information fusion | Fuses source information through trust, updates trust from losses, and derives a tractable LP; wildfire resource-allocation application | Useful if city demand sources have different reliability and parametric structure |
| Sequential charging-station location | Two-/multi-stage stochastic planning with choice-driven growth; conic reformulation and accelerating inequalities | Informs phased entry and demand growth; it is a stochastic location application rather than the same trust-fusion model |

## Shared decision principle

```math
\min_a\sup_{P\in\mathcal U(P_1,\ldots,P_K;\,\text{trust})}\mathbb E_P[c(a,D)].
```

This is a schematic summary: the papers use different constructions of $\mathcal U$. Source trust, transport radii, and dynamic updating are not interchangeable parameters. If introduced to robotaxi planning, source scope, bias, and reliability must first be defined on comparable demand units.

## Documents and their contents

- **[01_optimization_with_multi-sourced_information_and_unknown_reliability2501.07057v2.pdf](01_optimization_with_multi-sourced_information_and_unknown_reliability2501.07057v2.pdf)** — Multi-reference Wasserstein DRO combines sources with unknown reliability; studies dynamic trust, probability dominance, and linear reformulation.
- **[02_Distributionally_Robust_resource_allocation_with_trust-aided_parametric_information_fusion2411.01428v1.pdf](02_Distributionally_Robust_resource_allocation_with_trust-aided_parametric_information_fusion2411.01428v1.pdf)** — Trust-aided parametric fusion and loss-based trust updates for robust resource allocation; tractable LP and wildfire application.
- **[03_Sequential_Charging_Station_Location_Optimization_under_Uncertain_charging_behavior_and_user_growth2411.01416v1.pdf](03_Sequential_Charging_Station_Location_Optimization_under_Uncertain_charging_behavior_and_user_growth2411.01416v1.pdf)** — Sequential charging locations under uncertain choice/growth; multi-stage value, conic reformulation, and accelerating cuts.


---

[Parent guide](../README.md) · [Project overview](../../../README.md)
