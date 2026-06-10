# A Survey of Contextual Optimization Methods for Decision-Making under Uncertainty

## One-Sentence Summary

This survey explains how contextual information can be used to improve decisions under uncertainty, and it emphasizes that prediction models should be evaluated by decision quality, not only by predictive accuracy.

## 1. Big Picture

Contextual stochastic optimization studies decision-making when some information is observed before the decision is made.

In classical stochastic optimization, we often solve:

    minimize_x E[c(x, ξ)]

The decision `x` is chosen before observing uncertainty `ξ`.

In contextual stochastic optimization, before choosing the decision, we observe context `z`.

Then the decision can depend on `z`:

    minimize_x E[c(x, ξ) | z]

or more generally, we learn a policy:

    x = π(z)

where `π` maps context to decisions.

The core idea is:

> If the distribution of uncertainty changes with context, then the decision should also change with context.

## 2. Why Context Matters

Ignoring context means making one average decision.

But many operational decisions should depend on current conditions.

Examples:

### Logistics

Demand may depend on:

- location;
- day of week;
- weather;
- road conditions;
- military operational tempo;
- supply disruption status.

### Emergency Response

Resource needs may depend on:

- wildfire weather;
- wind direction;
- population density;
- evacuation status;
- terrain;
- infrastructure vulnerability.

### Healthcare

Treatment or staffing decisions may depend on:

- patient characteristics;
- hospital occupancy;
- time of day;
- disease severity.

### Transportation

Travel time and demand may depend on:

- traffic;
- time;
- events;
- weather;
- spatial region.

Therefore, contextual optimization is not simply about predicting uncertainty. It is about using context to choose better decisions.

## 3. Conditional Distribution View

The key mathematical shift is from the unconditional distribution:

    P(ξ)

to the conditional distribution:

    P(ξ | z)

The decision should be optimized under the conditional distribution.

This means two contexts may lead to different decisions even if the optimization problem structure is the same.

For example:

    High-risk context → allocate more resources.
    Low-risk context → allocate fewer resources.

This is similar to statistical modeling, but the final goal is not prediction accuracy. The final goal is decision quality.

## 4. Prediction versus Decision Quality

One of the most important lessons from the survey is:

> Better prediction does not always imply better decisions.

A prediction model can have low average prediction error but still lead to bad decisions if it makes mistakes in decision-critical regions.

For example:

- underpredicting demand in a high-penalty region may be very costly;
- overpredicting demand in a low-penalty region may not matter much;
- errors near a capacity threshold may matter more than errors far from the threshold;
- errors that change the optimal decision are more important than errors that do not.

Therefore, contextual optimization should be evaluated using decision metrics, not only prediction metrics.

Prediction metrics:

- mean squared error;
- mean absolute error;
- classification accuracy;
- log loss.

Decision metrics:

- realized cost;
- regret;
- revenue;
- service level;
- unmet demand;
- feasibility violation;
- robustness;
- policy stability.

This distinction is directly relevant to applied statistics, because it requires thinking beyond standard predictive modeling.

## 5. Main Methodological Frameworks

The survey organizes contextual optimization methods into different frameworks.

The major categories can be understood as:

1. estimate-then-optimize;
2. weighted sample average approximation;
3. direct policy learning;
4. decision-focused learning.

These frameworks differ in how tightly the learning model and the optimization problem are connected.

## 6. Estimate-Then-Optimize

Estimate-then-optimize is the most intuitive approach.

Step 1:

Estimate the conditional distribution:

    P(ξ | z)

Step 2:

Solve the optimization problem using that estimated distribution:

    minimize_x E[c(x, ξ) | z]

This approach is modular.

Statistical tools can be used in the estimation step:

- regression;
- generalized linear models;
- random forests;
- gradient boosting;
- neural networks;
- Bayesian models;
- quantile regression;
- conditional density estimation.

Advantages:

- easy to understand;
- easy to implement;
- interpretable;
- compatible with standard statistics and machine learning.

Disadvantages:

- the prediction model may ignore the downstream optimization objective;
- the best predictive model may not produce the best decision;
- uncertainty estimates may be poorly calibrated;
- overfitting in prediction can lead to unstable decisions.

This approach is close to many practical workflows.

## 7. Weighted Sample Average Approximation

Weighted SAA avoids estimating a full conditional distribution.

Instead, it uses historical samples and assigns larger weights to samples whose contexts are similar to the current context.

For a new context `z`, historical observations with contexts close to `z` receive higher weight.

Then the optimization problem is solved using a weighted empirical distribution.

Intuition:

    Use past situations similar to the current situation more heavily.

Examples:

- k-nearest neighbors;
- kernel weighting;
- random forest weights;
- local regression weights;
- tree-based partitions.

This method connects strongly to nonparametric statistics.

Advantages:

- flexible;
- does not require a full parametric distribution;
- intuitive;
- useful when similar historical contexts exist.

Disadvantages:

- can suffer in high dimensions;
- performance depends on the distance metric;
- may require many samples;
- weights can be unstable if data are sparse.

## 8. Direct Policy Learning

Direct policy learning tries to learn a decision rule directly.

Instead of estimating `P(ξ | z)`, it learns:

    π(z) = decision

The training objective is based on decision loss.

This approach asks:

> Which decision policy performs best across observed contexts and outcomes?

Advantages:

- directly aligned with decision performance;
- avoids unnecessary prediction of the full uncertainty distribution;
- may perform well when the optimal decision has simpler structure than the full conditional distribution.

Disadvantages:

- harder to train;
- may require solving difficult empirical risk minimization problems;
- less interpretable;
- can overfit;
- may be computationally heavy.

## 9. Decision-Focused Learning

Decision-focused learning trains a prediction model with the downstream optimization problem in mind.

Instead of training the prediction model to minimize MSE or another predictive loss, it trains the model to minimize decision loss after optimization.

Pipeline:

    context z
    → prediction model
    → optimization problem
    → decision x
    → decision loss

The prediction model is updated based on the decision loss.

This is powerful because it aligns prediction with the final objective.

However, it is technically difficult because it may require differentiating through an optimization problem.

Advantages:

- prediction is aligned with decision quality;
- useful when standard prediction metrics are not decision-relevant.

Disadvantages:

- computational complexity;
- differentiability issues;
- possible instability;
- harder interpretation;
- requires careful evaluation.

## 10. Sequential Learning and Optimization versus Integrated Learning and Optimization

In our discussion, we connected contextual optimization with the broader distinction between SLO and ILO.

### 10.1 Sequential Learning and Optimization

SLO separates learning and optimization.

    learn or estimate uncertainty
    → plug into optimization
    → solve decision problem

This is easier and more interpretable.

Examples:

- estimate demand distribution, then solve facility location;
- generate scenarios, then solve stochastic programming;
- forecast returns, then solve portfolio optimization.

The charging station paper is closest to this structure because it creates demand scenarios and then solves a two-stage or multi-stage stochastic programming model.

### 10.2 Integrated Learning and Optimization

ILO integrates learning with the decision objective.

    train the learning model to improve downstream decisions

This can produce better decision quality, but it is more complex and less transparent.

The charging station paper is not an ILO paper because it does not train the demand model end-to-end through the station location objective.

This distinction helped clarify the correct classification of the charging station paper.

## 11. Connection to the Charging Station Paper

The charging station paper is not primarily a contextual optimization survey paper, but it connects to contextual optimization in several ways.

The paper uses:

- demand growth scenarios;
- spatial locations;
- user choice behavior;
- station type;
- multi-stage stochastic programming.

The current paper assumes a scenario tree for future demand growth.

A contextual extension could model demand growth as depending on:

- population density;
- income;
- existing EV adoption;
- traffic flow;
- policy incentives;
- location type;
- distance to urban centers;
- charging infrastructure availability.

This would make scenario generation more context-aware.

Also, the MNL user choice model already uses contextual features such as distance and station type. However, the paper treats MNL parameters as fixed. A statistical extension could estimate and propagate uncertainty in those parameters.

## 12. Connection to MR-DRO

Contextual optimization also connects naturally to the MR-DRO papers.

In MR-DRO, each source has a trust value.

But in reality, source reliability may depend on context.

For example:

- drone data may be reliable in clear weather but unreliable in smoke;
- satellite data may be reliable for broad spatial patterns but less reliable for local details;
- social media may be useful in urban regions but noisy in rural areas;
- official reports may be accurate but delayed;
- simulation models may work well in familiar conditions but poorly in extreme events.

This suggests a natural extension:

    source trust = t_h(z)

where trust depends on context.

This idea combines:

- contextual stochastic optimization;
- source reliability modeling;
- MR-DRO;
- data-driven robust decision-making.

## 13. Contextual DRO

Contextual optimization and DRO answer different but related questions.

Contextual optimization asks:

    How should the decision change when we observe context?

DRO asks:

    How can we make a decision robust when the distribution is uncertain?

A combined framework could ask:

    How can we make context-dependent decisions that are robust to distributional uncertainty?

Possible structure:

    observe context z
    → estimate context-dependent reference distribution P_hat(z)
    → build context-dependent ambiguity set around P_hat(z)
    → solve robust decision problem

This could lead to:

- context-dependent ambiguity sets;
- context-dependent Wasserstein radius;
- context-dependent source trust;
- robust contextual policies;
- distribution shift-aware contextual optimization.

## 14. Why This Is Relevant to Statistics

Contextual optimization requires statistical tools.

Possible statistical tasks:

- estimating conditional distributions;
- selecting useful context variables;
- avoiding overfitting;
- calibrating predictive distributions;
- validating decision policies;
- measuring out-of-sample decision quality;
- estimating uncertainty in learned policies.

The major difference from standard statistics is that evaluation should be decision-focused.

This means that a statistics student needs to ask:

> Does the model improve the decision, not only the prediction?

## 15. My Understanding

My understanding is:

> Contextual stochastic optimization is about adapting decisions to observed information. It is not enough to know the average distribution of uncertainty. If useful context is available, the decision should depend on the conditional distribution of uncertainty given that context.

The most important lesson is that prediction and optimization are connected but not identical.

The final objective is decision quality.

## 16. Possible Statistical Contributions

### 16.1 Conditional Distribution Estimation

I can help estimate distributions such as:

- demand given location and time;
- travel time given traffic and weather;
- resource need given operational context;
- source error given context.

### 16.2 Decision-Oriented Model Comparison

I can compare predictive models based on decision performance.

For example:

- model A has lower MSE;
- model B leads to lower realized cost.

The better model for optimization may be model B.

### 16.3 Context-Dependent Trust

This is one of the most interesting connections to MR-DRO.

Instead of fixed source trust, estimate:

    t_h(z)

Possible contexts:

- region;
- weather;
- time;
- sensor condition;
- information delay;
- operational environment.

### 16.4 Simulation Design

I can design simulation experiments where context affects:

- demand distribution;
- source reliability;
- error bias;
- variance;
- distribution shift;
- decision cost.

Then I can test whether contextual trust or contextual DRO improves decision quality.

### 16.5 Out-of-Sample Policy Evaluation

I can evaluate policies using:

- train/test split;
- rolling evaluation;
- bootstrap;
- paired policy comparison;
- regret;
- realized cost.

## 17. Possible Research Questions

1. When does contextual information significantly improve decision quality?
2. How should contextual optimization models be evaluated out of sample?
3. Can source reliability in MR-DRO be context-dependent?
4. Can contextual prediction be combined with Wasserstein DRO?
5. How do we prevent overfitting in contextual decision policies?
6. Does better prediction accuracy always reduce decision cost?
7. How should we choose contextual features for logistics resource allocation?
8. Can ambiguity radius be context-dependent?
9. Can contextual information help choose which source to trust?
10. How can contextual optimization be applied to emergency logistics?

## 18. Possible Statement for Professor Shen

I am interested in the connection between contextual optimization and multi-source DRO. In particular, I wonder whether source reliability should be modeled as context-dependent. For example, a source may be reliable under some operational conditions but unreliable under others. As a statistics student, I could help explore this through conditional prediction models, simulation studies, and out-of-sample decision evaluation.

## 19. Final Takeaway

The main lesson from contextual stochastic optimization is that uncertainty should not always be modeled unconditionally.

If useful context is available, decisions should adapt to that context.

For my research preparation, the most promising connection is to combine contextual information with source reliability and robust optimization.
