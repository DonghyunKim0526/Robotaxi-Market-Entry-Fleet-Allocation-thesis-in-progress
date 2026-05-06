# Contextual Stochastic Optimization Tutorial

## One-Sentence Summary

This tutorial introduces contextual stochastic optimization, where decisions are made after observing covariates, and the goal is to use context to improve decisions under uncertainty.

## 1. Big Picture

In classical stochastic optimization, we make a decision under uncertainty using an unconditional distribution.

A typical formulation is:

    minimize_x E[c(x, ξ)]

In contextual stochastic optimization, before making the decision, we observe context `z`.

The decision can then depend on the context:

    minimize_x E[c(x, ξ) | z]

or we learn a policy:

    x = π(z)

This means the decision is adapted to the observed situation.

## 2. Simple Example

Suppose we need to allocate emergency resources.

Without context, we may allocate resources based on average demand.

With context, we can use information such as:

- weather;
- region;
- time of day;
- road conditions;
- population density;
- sensor reports;
- recent incidents.

Then the allocation can change depending on the current situation.

This is the key motivation of contextual stochastic optimization.

## 3. Why Conditional Expectation Matters

The important shift is from:

    E[c(x, ξ)]

to:

    E[c(x, ξ) | z]

This means that uncertainty is not treated as the same across all situations.

Instead, the distribution of `ξ` changes depending on context.

For example:

- demand distribution may differ by region;
- travel time distribution may differ by weather;
- supply disruption probability may differ by operational condition.

## 4. Learning a Decision Policy

A policy maps context to decisions:

    π: context → decision

The goal is to learn a policy that performs well over future contexts and outcomes.

This is different from learning a prediction model only.

The policy should be evaluated by the cost or reward of the decision.

## 5. Estimate-Then-Optimize

One straightforward approach is:

1. estimate the conditional distribution of uncertainty given context;
2. solve the optimization problem using that estimated distribution.

This approach is easy to understand.

For example:

    estimate demand distribution given region and weather
    → solve resource allocation problem

This connects naturally to applied statistics.

Possible tools:

- linear regression;
- generalized linear models;
- random forests;
- gradient boosting;
- neural networks;
- Bayesian models;
- quantile regression;
- conditional density estimation.

## 6. Weighted Empirical Methods

Another approach is to use historical samples similar to the current context.

For a new context, assign larger weights to past observations with similar contexts.

Then solve a weighted sample average approximation problem.

This is similar to nonparametric regression.

Examples:

- k-nearest neighbors;
- kernel weighting;
- local regression;
- random forest weights.

The advantage is that we do not need to fully specify a parametric conditional distribution.

## 7. Direct Policy Learning

Instead of first estimating the distribution, direct policy learning tries to learn the decision rule directly.

This can be written as:

    choose policy π to minimize average decision loss

This is more directly aligned with the decision objective.

However, it may be more difficult to train and interpret.

## 8. Decision-Focused Learning

Decision-focused learning trains a prediction model so that it produces good decisions after optimization.

The loss function is based on decision quality rather than pure prediction error.

This is important because small prediction errors may matter a lot in some regions and very little in others.

For example, in resource allocation:

- underpredicting high-priority demand may be very costly;
- overpredicting low-priority demand may be less serious.

Therefore, prediction models should sometimes be trained with the downstream optimization task in mind.

## 9. Key Lesson from the Tutorial

The key lesson is:

> The purpose of contextual stochastic optimization is not merely to predict uncertainty. The purpose is to make better decisions using contextual information.

This means that evaluation should focus on decision quality.

## 10. Relation to Charging Station Paper

The charging station paper uses demand scenarios and solves a multi-stage stochastic programming problem.

It is not exactly a contextual optimization paper in the decision-focused learning sense.

However, it shares the idea that better uncertainty modeling affects decisions.

The possible connection is:

- demand growth may depend on spatial and socioeconomic context;
- user choice may depend on distance and station characteristics;
- future demand scenarios could be generated conditionally on context.

A statistical extension could improve scenario generation using contextual features.

## 11. Relation to MR-DRO

Contextual optimization also connects to MR-DRO through source reliability.

In MR-DRO, each source has a trust value.

But source reliability may depend on context.

For example:

    trust of drone data = high when visibility is good
    trust of satellite data = low when cloud cover is high
    trust of social media = high in urban regions but low in rural regions

This suggests context-dependent trust:

    t_h(z)

This could combine contextual optimization with multi-source DRO.

## 12. My Understanding

My current understanding is:

> Contextual stochastic optimization is the optimization version of conditional prediction. It asks how the optimal decision should change when the conditional distribution of uncertainty changes with observed features.

This is different from simply forecasting `ξ`.

The important question is whether using context improves the final decision.

## 13. Statistical Contribution

As a statistics student, I can contribute through:

- conditional distribution estimation;
- feature selection;
- model comparison;
- calibration;
- uncertainty quantification;
- out-of-sample policy evaluation;
- simulation studies;
- context-dependent trust modeling.

## 14. Possible Research Directions

1. Context-dependent trust in multi-source DRO.
2. Conditional Wasserstein ambiguity sets.
3. Robust contextual optimization under distribution shift.
4. Decision-focused evaluation of prediction models.
5. Scenario generation using contextual features.
6. Rolling-horizon contextual decision policies.
7. Logistics resource allocation with real-time contextual information.

## 15. Questions for Discussion

1. Is contextual trust a reasonable extension of the MR-DRO framework?
2. Should trust depend on source, region, time, or operational condition?
3. What data would be needed to estimate context-dependent trust?
4. If data are unavailable, can simulation be used to test this idea?
5. How can we evaluate contextual optimization policies out of sample?

## 16. Final Takeaway

This tutorial provides the conceptual foundation for understanding how context can improve stochastic optimization.

For my research direction, the most interesting connection is using contextual information not only to predict uncertainty, but also to determine which information sources should be trusted under different conditions.
