# Contextual optimization: concepts

## The central idea

An unconditional model applies the same demand distribution to different cities. A contextual model first observes city features $X=x$ and chooses a decision appropriate for that conditional demand.

```math
\min_q\mathbb E[c(q,D)]\quad\longrightarrow\quad
q^*(x)\in\arg\min_q\mathbb E[c(q,D)\mid X=x].
```

## Three building blocks in the illustrated notes

1. **C2 — method map:** estimate a distribution and optimize, weight similar historical observations, or train directly for decision cost. These are different ways to couple learning and optimization.
2. **C3 — residual recipe:** fit a response function, collect prediction residuals, and attach them to a new city's prediction to generate scenarios. Leave-one-out variants reduce reuse of training residuals.
3. **C4 — distributional protection:** place an ambiguity set around the residual/scenario distribution when the empirical distribution is uncertain. Choose robustness using validation, not just training fit.

For robotaxi fleets, $c(q,D)=c^+(q-D)_++c^-(D-q)_+$ is the basic surplus/shortage trade-off (capacity scaling is restored in the main formulation). The actual project keeps $M$ fixed and models logit $p$, rather than using an unrestricted additive model on trip counts.

The English concept PDF and Korean translation explain the same method progression. They are visual learning notes, not new empirical results or proof that a fitted city model satisfies the cited assumptions.

## Documents and their contents

- **[contextual stochastic optimization concept.pdf](contextual%20stochastic%20optimization%20concept.pdf)** — Illustrated explanation of conditional decisions, C2 method families, C3 residual scenarios, and C4 robustness.
- **[translation.pdf](translation.pdf)** — 조건부 결정, 예측·최적화 방법군, 잔차 시나리오, 분포 강건성을 설명하는 개념 문서의 한글판입니다.


---

[Parent guide](../README.md) · [Project overview](../../../../README.md)
