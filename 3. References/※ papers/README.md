# Supporting papers: concepts and reference map

The collection is organized below by **concept → relevant papers → their different approaches → use in this research**. These methodological references explain modeling choices; they do not by themselves calibrate robotaxi demand or costs.

## 1. Contextual optimization: decisions that use observed features

**Concept:** use information available before the decision to describe demand conditional on a new city's characteristics. Prediction and optimization can be linked in several ways.

| Reference | How it explains the concept | Relevance here |
|---|---|---|
| [C1 — Delage, contextual optimization tutorial](C.%20contextual_stochastic_optimization/C1_ContextualOptimization_Tutorial_ICSP.pdf) | Introduces why revealed context should change a decision and how prediction connects to stochastic optimization. | Entry point for the city-context → demand → deployment pipeline. |
| [C2 — Sadana et al., survey of contextual optimization](C.%20contextual_stochastic_optimization/C2_survey%20of%20contextual%20optimization%20methods%201-s2.0-S0377221724002200-main.pdf) | Organizes sequential prediction/optimization, weighted scenarios, integrated learning, and policy approaches under one framework. | Places the current residual-based approach among alternatives; the survey is a method map, not one estimator. |

## 2. Empirical residuals: turning a prediction into scenarios

**Concept:** fit the response to context, then use residual variation to generate demand scenarios at new context values rather than optimizing only a point prediction.

| Reference | How it explains the concept | Relevance here |
|---|---|---|
| [C3 — Kannan, Bayraksan & Luedtke, covariate-informed SAA](C.%20contextual_stochastic_optimization/C3_Kannan_Data-Driven%20Sample%20Average%20Approximation%20with%20Covariate%20Info.pdf) | Develops residual-based and leave-one-out SAA frameworks; studies consistency, convergence, and finite-sample behavior under assumptions. | Supports the residual-scenario logic behind ER-SAA. This project applies residuals on the logit choice scale before converting to trip demand. |

## 3. Distributional robustness: uncertainty about the scenario distribution

**Concept:** protect against a family of plausible distributions. Reweighting existing outcomes, transporting outcomes, and combining source neighborhoods represent different ambiguity models.

| Reference | How it explains the concept | Relevance here |
|---|---|---|
| [C4 — Kannan, Bayraksan & Luedtke, residual-based DRO](C.%20contextual_stochastic_optimization/C4_Kannan_Residuals-based%20distributionally%20robust%20optimization.pdf) | Combines prediction and residual-based ambiguity sets; analyzes statistical properties and cross-validation approaches to set sizing. | Connects residual learning with protection against limited data or prediction misspecification; assumptions and tuning still need validation. |
| [Kuhn, Shafiee & Wiesemann, DRO survey](B.%20distributionally_robust_optimization/02_distributionally-robust-optimization.pdf) | Provides a broad treatment of ambiguity sets, duality, tractable formulations, and statistical/regularization connections. | Reference for explaining the robustness model and the conditions behind theoretical guarantees. |
| [Blanchet et al., unifying DRO via optimal transport](B.%20distributionally_robust_optimization/01_Unifying_Distributionally_Robust_Optimization_via_Optimal_Transport_Theory2308.05414v2.pdf) | Uses generalized optimal transport with conditional moment constraints to connect likelihood-ratio and outcome perturbations. | Clarifies why probability reweighting and Wasserstein movement are different modeling choices. |
| [Rychener et al., Wasserstein DRO with heterogeneous sources](B.%20distributionally_robust_optimization/03_Wasserstein_Distributionally_Robust_Optimization_with_Heterogeneous_Data_Sources2407.13582v1.pdf) | Intersects transport neighborhoods around biased data sources and studies how prior bias information affects decisions. | A possible source-aware extension; requires source-specific information rather than treating all observations as exchangeable. |

**Current implementation:** the robotaxi model uses a CVaR-type formulation over fixed residual-generated scenarios. It does not implement all ambiguity sets in these papers or automatically inherit every statistical guarantee they establish.

## 4. Decision-dependent demand: decisions also change what is demanded

**Concept:** city features are exogenous, but opening a site or changing capacity/service can alter demand. This requires learning decision responses, not merely conditioning on fixed context.

| Reference | How it explains the concept | Relevance here |
|---|---|---|
| [Sun, Yu & Bayraksan, contextual EV charging-station location](C.%20contextual_stochastic_optimization/EV_charging_station.pdf) | Models demand depending on both context and first-stage location/capacity; uses two-step demand learning and empirical-residual decision-dependent SAA, with synthetic and New York applications. | Template for a future decision-dependent extension. The current robotaxi ER-DRO notebook has exogenous demand; this EV paper uses ER-DD-SAA, not the same implemented CVaR model. |

## 5. Multi-source information: reliability and trust in demand inputs

**Concept:** sources may disagree or have different reliability. Information fusion can explicitly represent source trust instead of indiscriminately pooling data.

| Reference | How it explains the concept | Relevance here |
|---|---|---|
| [Guo, Jiang & Shen, multi-sourced information with unknown reliability](A.%20multi_sourced_data/01_optimization_with_multi-sourced_information_and_unknown_reliability2501.07057v2.pdf) | Develops multi-reference Wasserstein DRO, nonparametric fusion, dynamic trust updates, and probability dominance; gives a linear reformulation in a linear setting. | Framework to consider when several demand sources disagree; not implemented in the current single-residual-sample experiment. |
| [Guo et al., trust-aided parametric information fusion](A.%20multi_sourced_data/02_Distributionally_Robust_resource_allocation_with_trust-aided_parametric_information_fusion2411.01428v1.pdf) | Uses trust-weighted parametric source information with loss-based trust updates; develops tractable resource-allocation models and a wildfire application. | Shows a different, parametric route to source fusion and how trust may evolve with observed performance. |

## 6. Location and allocation applications: time, coverage, and feasibility

**Concept:** opening locations and allocating resources can interact with demand growth, service coverage, operational constraints, and risk preferences.

| Reference | How it explains the concept | Relevance here |
|---|---|---|
| [Shen et al., sequential charging-station location](A.%20multi_sourced_data/03_Sequential_Charging_Station_Location_Optimization_under_Uncertain_charging_behavior_and_user_growth2411.01416v1.pdf) | Integrates user choice and uncertain growth in two-/multi-stage planning; derives a conic representation and accelerating inequalities. | Informs phased expansion and the value of adapting to future demand; despite its storage folder, it is primarily a sequential-planning reference. |
| [Basciftci, Yu & Shen, disease-spread resource distribution](D.%20other_related_papers/01_Resource%20Distribution%20Inder%20Spatiotemporal%20Uncertainty%20of%20Disease%20Spread.pdf) | Compares stochastic programming and moment-based DRO while balancing facility/logistics costs, coverage, and equity. | Structural example of expected-cost versus worst-case-service trade-offs, with constraints beyond the current robotaxi model. |
| [Wu et al., spaceport facility location](D.%20other_related_papers/02_Spaceport%20Facility%20Location%20Planning.pdf) | Links site selection and launch allocation to population, trajectories, air-traffic effects, and operational restrictions. | Illustrates why location choices must include physical feasibility and external impacts, not just expected demand. |

## Concept notes and suggested reading order

- [Illustrated contextual-optimization notes](C.%20contextual_stochastic_optimization/concept/contextual%20stochastic%20optimization%20concept.pdf) · [Korean translation](C.%20contextual_stochastic_optimization/concept/translation.pdf): project learning notes explaining C2's method map, C3's residual recipe, and C4's robustification; not additional research papers.
- Start with **C1/C2 → C3 → C4** to follow context, residual scenarios, and robustness. Read the **EV-location paper** for decision dependence; use the **DRO survey** for ambiguity-set foundations and the **multi-source papers** when source reliability becomes part of the model.

## Storage folders

- [A. multi_sourced_data](A.%20multi_sourced_data/): multi-source/trust papers and the sequential charging-location application.
- [B. distributionally_robust_optimization](B.%20distributionally_robust_optimization/): DRO foundations and heterogeneous-source transport models.
- [C. contextual_stochastic_optimization](C.%20contextual_stochastic_optimization/): tutorial, survey, residual SAA/DRO, EV-location application, and concept notes.
- [D. other_related_papers](D.%20other_related_papers/): resource-distribution and spaceport applications.

[References overview](../README.md) · [Project overview](../../README.md)
