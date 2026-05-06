# Wasserstein Distributionally Robust Optimization with Multiple Biased Data Sources

## One-Sentence Summary

This paper studies how to use multiple biased data sources in a Wasserstein DRO framework, showing that even biased sources may be useful if their bias and uncertainty are modeled carefully.

## 1. Big Picture

In practice, data sources are often biased.

A dataset may not represent the true target distribution because it comes from a different population, a different region, a different time period, or a different measurement system.

However, biased data may still contain useful information.

The key question is:

> How can a decision-maker use multiple biased data sources without blindly trusting any one of them?

This paper is closely related to the multi-source DRO papers because it also considers multiple sources, imperfect information, and Wasserstein ambiguity sets.

## 2. Why Biased Data Sources Matter

Real datasets often differ from the target distribution.

Examples:

- sensor data may have measurement bias;
- social media data may overrepresent certain populations;
- simulation outputs may be generated under simplified assumptions;
- historical data may come from a different environment;
- expert forecasts may be systematically optimistic or pessimistic.

If we directly optimize using a biased empirical distribution, the decision may perform poorly on the actual target distribution.

DRO provides a way to protect against this issue.

## 3. Main Modeling Idea

The paper uses Wasserstein DRO with multiple empirical distributions.

Each empirical distribution comes from a different data source.

Rather than assuming one source is correct, the model considers ambiguity sets related to several biased sources.

The Wasserstein distance is useful because it allows the true distribution to be near but not identical to each source distribution.

Intuitively:

    biased source distributions
    → Wasserstein neighborhoods
    → plausible target distributions
    → robust decision

## 4. Relation to MR-DRO

This paper is related to MR-DRO but focuses more on biased data sources.

MR-DRO with trust asks:

> How much should we trust each source?

This paper asks:

> How can we use multiple sources when each may be biased relative to the target distribution?

Both approaches recognize that multiple sources are imperfect.

The difference is that trust-based MR-DRO emphasizes reliability weights, while biased-source DRO emphasizes distributional neighborhoods around source distributions.

## 5. Why Wasserstein Distance Is Natural Here

Wasserstein distance is natural because bias may shift the actual values of the distribution.

For example:

- a source may overestimate demand in one region;
- a source may underestimate tail risk;
- a source may be spatially shifted;
- a source may come from a related but not identical population.

A divergence that only reweights existing samples may not fully capture these shifts.

Wasserstein distance allows probability mass to move in the uncertainty space, which is useful for modeling biased samples.

## 6. My Understanding

In my own words:

> Even if each data source is biased, we may still be able to use them together by modeling how far each source could be from the true distribution.

This is important because real decision-makers often cannot wait for perfect data.

The question becomes how to use imperfect data responsibly.

## 7. Statistical Questions

The paper raises several statistical questions.

1. How can source bias be estimated?
2. What if the true target distribution is never observed?
3. How large should the Wasserstein neighborhood around each source be?
4. Should different sources have different ambiguity radii?
5. How can we detect whether two sources share the same bias?
6. How should correlated source errors be handled?

## 8. Connection to My Discussion with MR-DRO

In our discussion of MR-DRO, one important point was that if all sources are biased in the same direction, trust weighting alone may not solve the problem.

This biased-data-source perspective is relevant because it focuses on the fact that all reference distributions may be imperfect.

Therefore, a useful extension may combine:

- trust weights;
- source-specific bias modeling;
- source-specific Wasserstein radii;
- out-of-sample validation.

## 9. Possible Contribution as a Statistics Student

I could contribute by studying:

- source bias estimation;
- source error distribution analysis;
- source-specific radius calibration;
- simulation with controlled bias;
- correlated source errors;
- sensitivity of robust decisions to bias assumptions;
- comparison between trust weighting and biased-source ambiguity sets.

If real data are unavailable, simulation-based experiments can still be useful.

## 10. Simulation Ideas

Possible simulation factors:

- one source unbiased, one source biased;
- all sources biased in the same direction;
- sources biased in opposite directions;
- source variance differences;
- source bias changes over time;
- source errors are correlated;
- sample sizes differ by source.

Evaluation metrics:

- realized loss;
- regret;
- robustness;
- stability of source weights;
- sensitivity to ambiguity radius.

## 11. Possible Research Questions

1. Can trust weighting and source-specific Wasserstein radii be combined?
2. How should source bias affect trust updates?
3. What happens when a biased source has low variance but high systematic error?
4. Can context explain when a source is biased?
5. How can we validate decisions when the target distribution is only partially observed?

## 12. Final Takeaway

This paper reinforces a key theme across the literature: data sources are useful but imperfect.

For my research preparation, the important lesson is that source reliability is not only about variance or prediction accuracy. Bias matters too.

A strong statistical contribution would be to analyze how bias, variance, correlation, and nonstationarity in multiple sources affect DRO decisions.
