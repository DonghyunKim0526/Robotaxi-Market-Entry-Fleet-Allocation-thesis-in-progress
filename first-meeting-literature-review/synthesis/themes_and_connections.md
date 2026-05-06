
---

## `synthesis/themes_and_connections.md`

```markdown
# Themes and Connections Across the Papers

## 1. Overall Theme

The papers I reviewed are all about decision-making under uncertainty.

The common question is:

> How can we make better operational decisions when the future is uncertain and the available data are imperfect?

The papers approach this question from different angles:

- multi-source information fusion;
- distributionally robust optimization;
- trust update mechanisms;
- stochastic programming;
- contextual stochastic optimization;
- sequential infrastructure planning.

## 2. Multi-Sourced Information

The MR-DRO papers focus on situations where multiple sources provide information about the same uncertain parameter.

The key challenge is that the sources may differ in:

- accuracy;
- bias;
- variance;
- relevance;
- timeliness;
- reliability over time.

A simple average of sources may be inappropriate because not all sources should be trusted equally.

The important modeling idea is to use source-level trust to construct a reference distribution for optimization.

## 3. Trust Is a Statistical Object

One major takeaway is that trust should not be viewed only as an optimization parameter.

Trust is closely related to statistical concepts such as:

- prediction error;
- bias;
- variance;
- calibration;
- uncertainty;
- nonstationarity;
- source correlation.

This creates a natural role for applied statistics.

## 4. DRO as Protection Against Distributional Error

DRO protects against the fact that the estimated or fused distribution may be wrong.

Instead of trusting one distribution completely, DRO considers a neighborhood of plausible distributions.

The Wasserstein ambiguity set is important because it allows the model to hedge against distributional misspecification.

However, DRO also raises statistical questions:

- How large should the ambiguity set be?
- How conservative is the resulting solution?
- How should the radius be calibrated?
- How should we evaluate out-of-sample performance?

## 5. Stochastic Programming versus DRO

The charging station paper is different from the MR-DRO papers.

It uses multi-stage stochastic programming rather than DRO.

The model assumes a scenario tree for future demand growth and optimizes expected performance over scenarios.

The MR-DRO papers focus on ambiguity around the distribution, while the charging station paper focuses on sequential decision-making under scenario-based uncertainty.

In simple terms:

```text
Stochastic programming:
Assume a scenario distribution and optimize expected performance.

DRO:
Do not fully trust one distribution; optimize worst-case performance over nearby distributions.

Multi-stage stochastic programming:
Allow future decisions to adapt as uncertainty is gradually revealed.