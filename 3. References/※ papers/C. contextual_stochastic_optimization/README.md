# Contextual stochastic optimization

## From city features to decisions

$$\min_a\mathbb E[c(a,D)\mid X=x],\qquad
\hat D^s(x)=\hat f(x)+\hat\varepsilon_s.$$

The displayed scenario equation is the additive residual idea; the robotaxi implementation applies residuals on the **logit scale** and then maps back through a sigmoid.

| Document | Main contribution | Role in this project |
|---|---|---|
| C1 tutorial | Motivation and ways of using observed context in stochastic decisions | Entry point for the prediction–decision pipeline |
| C2 survey | Organizes sequential prediction/optimization, weighted scenarios, integrated learning, and policy methods | Explains the method landscape and distinctions |
| C3 residual SAA | Uses learned predictions and empirical or leave-one-out residuals; consistency and finite-sample results under assumptions | Basis for generating conditional city scenarios |
| C4 residual DRO | Robustifies residual distributions; considers several ambiguity sets and cross-validation sizing | Basis for accounting for limited data and misspecified prediction |
| EV charging-station location | Demand depends on exogenous context and first-stage location/capacity; two-step demand learning and ER-DD-SAA | Template for a future decision-dependent extension, not the present implementation |

## Key distinction

Contextual demand is $D(x,\varepsilon)$: city features affect the scenarios, which are fixed before solving. Decision-dependent demand is $D(x,a,\varepsilon)$: opening sites or changing capacity changes the demand distribution. Prediction accuracy alone is not decision quality; evaluate the chosen decision's cost on independent outcomes.

The concept notes below give an illustrated explanation. The present experiment uses one exogenous context, logit residuals, and CVaR reweighting; it does not implement every estimator or guarantee discussed in these papers.

## Documents and their contents

- **[C1_ContextualOptimization_Tutorial_ICSP.pdf](C1_ContextualOptimization_Tutorial_ICSP.pdf)** — Tutorial introducing decisions conditioned on observed features and the connection between prediction and optimization.
- **[C2_survey of contextual optimization methods 1-s2.0-S0377221724002200-main.pdf](C2_survey%20of%20contextual%20optimization%20methods%201-s2.0-S0377221724002200-main.pdf)** — Method taxonomy for contextual decisions, including sequential learning, weighted scenarios, integrated learning, and policy optimization.
- **[C3_Kannan_Data-Driven Sample Average Approximation with Covariate Info.pdf](C3_Kannan_Data-Driven%20Sample%20Average%20Approximation%20with%20Covariate%20Info.pdf)** — Residual and leave-one-out SAA frameworks with covariates; consistency, convergence, and finite-sample results under assumptions.
- **[C4_Kannan_Residuals-based distributionally robust optimization.pdf](C4_Kannan_Residuals-based%20distributionally%20robust%20optimization.pdf)** — Residual-based contextual DRO with several ambiguity sets, statistical analysis, and cross-validation for robustness sizing.
- **[EV_charging_station.pdf](EV_charging_station.pdf)** — Decision-dependent EV demand learning and two-stage station location using ER-DD-SAA, two-step regression, and synthetic/NY applications.


## Related folders

- [concept](concept/README.md)


---

[Parent guide](../README.md) · [Project overview](../../../README.md)
