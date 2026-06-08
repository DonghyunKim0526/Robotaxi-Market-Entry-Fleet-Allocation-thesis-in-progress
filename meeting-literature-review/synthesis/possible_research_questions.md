
---

## `synthesis/possible_research_questions.md`

```markdown
# Possible Research Questions

## 1. Source Reliability in Multi-Source DRO

How can we estimate or validate the reliability of multiple information sources when the true distribution is unknown?

Related questions:

- How should initial trust values be chosen?
- How sensitive are decisions to initial trust?
- How quickly should trust update after prediction errors?
- What happens if source reliability changes over time?
- What happens if multiple sources are biased in the same direction?

## 2. Statistical Interpretation of Trust

Can source trust be modeled as a statistical reliability parameter rather than only as an algorithmic weight?

Possible directions:

- Bayesian trust modeling;
- posterior distribution over source reliability;
- confidence intervals for source trust;
- precision-based source weights;
- region-specific or context-specific trust.

## 3. Context-Dependent Trust

In many applications, a source may be reliable in some contexts but unreliable in others.

For example:

- drone data may be more reliable in clear weather;
- satellite data may be less reliable under cloud cover;
- social media may be more useful in urban areas;
- official reports may be delayed but accurate.

Possible question:

> Can trust be modeled as a function of context rather than a fixed source-level weight?

## 4. Nonstationary Source Reliability

Source reliability may change over time.

Possible directions:

- change-point detection;
- rolling-window trust updates;
- variable-share trust update;
- adaptive learning rates;
- comparison of trust update rules under nonstationarity.

## 5. Source Correlation

Multiple sources may not be independent.

For example, two forecasting models may rely on similar raw data.

Possible question:

> How does correlation among source errors affect trust-weighted fusion and MR-DRO performance?

Possible methods:

- source error correlation analysis;
- factor models for source errors;
- clustering sources by error pattern;
- penalizing redundant sources.

## 6. Wasserstein Radius Calibration

The Wasserstein radius controls the conservativeness of DRO.

Possible questions:

- How should the radius be selected in practice?
- Can validation or bootstrap be used?
- How does radius choice affect out-of-sample loss?
- How does radius choice interact with source trust?

## 7. Simulation-Based Robustness Analysis

If real multi-source data are unavailable, direct trust estimation is impossible.

In that case, simulation-based validation is a realistic contribution.

Possible simulation factors:

- source bias;
- source variance;
- source correlation;
- heavy-tailed demand;
- non-Gaussian demand;
- number of historical events;
- source reliability change over time;
- misspecified trust update rules.

Main question:

> Under what data-generating conditions does MR-DRO perform well, and under what conditions does it fail?

## 8. Charging Station Paper Extensions

The charging station paper suggests several statistical research questions.

### Demand Scenario Generation

How should future EV demand scenarios be generated?

Possible alternatives:

- Gaussian growth;
- bootstrap;
- Bayesian posterior predictive scenarios;
- heavy-tailed growth;
- spatially correlated growth;
- policy shock scenarios.

### MNL Parameter Uncertainty

The MNL parameters are treated as fixed, but in practice they are estimated.

Questions:

- How sensitive are location decisions to MNL parameters?
- How should uncertainty in distance sensitivity be propagated?
- Would mixed logit improve realism?

### Rolling-Horizon Comparison

A practical planning system may re-optimize every year.

Question:

> How much value does the full multi-stage stochastic programming model add compared with rolling-horizon re-optimization?

## 9. Candidate Research Question

A possible research question I could discuss with Professor Shen is:

> How can we evaluate the robustness and failure modes of trust-aided multi-source DRO when source reliability, bias, variance, and correlation vary across time and context?

Another possible question is:

> How can contextual or statistical information be used to make source trust adaptive rather than fixed at the source level?

## 10. Questions for Professor Shen

1. Among these directions, which is most useful for the current projects?
2. Would it be better for me to start with simulation-based validation or literature review expansion?
3. Are there existing datasets or codebases that I could study?
4. Is source reliability modeling an open issue in the current multi-source DRO work?
5. Would rolling-horizon comparison be useful for the sequential charging station paper or related projects?
6. As a statistics student, should I focus more on uncertainty modeling, validation, or computational experiments?