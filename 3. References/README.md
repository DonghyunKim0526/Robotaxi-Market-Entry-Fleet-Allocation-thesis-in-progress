# References and parameter rationale

## Folder and document guide

| File / folder | What it explains |
|---|---|
| [A. cost_selection_rationale.pdf](A.%20cost_selection_rationale.pdf) | Why entry cost, vehicle cost, and surplus/shortage losses belong in the baseline objective; distinguishes literature structure from additional assumptions |
| [B. parameter_rationale_baseline.pdf](B.%20parameter_rationale_baseline.pdf) | How baseline parameter values and sensitivity levels are derived from reported observations, estimates, proxies, and synthetic assumptions |
| [※ translation](%E2%80%BB%20translation/README.md) | Korean A/B companions and [C. 모델 구조 가이드라인.pdf](%E2%80%BB%20translation/C.%20%EB%AA%A8%EB%8D%B8%20%EA%B5%AC%EC%A1%B0%20%EA%B0%80%EC%9D%B4%EB%93%9C%EB%9D%BC%EC%9D%B8.pdf), comparing baseline, contextual, robust, and decision-dependent model structures |
| [※ papers](%E2%80%BB%20papers/README.md) | Concept-classified methodological papers on residual learning, contextual optimization, DRO, source reliability, and related location/allocation applications |

## A. Why these cost components were selected

A explains the **structure of the objective**, not numerical calibration. It identifies which terms are adapted from literature, which use cost-classification guidance, and which are additional assumptions of this study.

| Baseline component | Main supporting references / reasoning | Modeling implication |
|---|---|---|
| Entry cost $F_cy_c$ | Sun, Yu & Bayraksan's EV-location model; Zhang et al.'s joint fleet/charging-system planning | Opening a market or supporting facility creates a fixed commitment separate from per-vehicle cost |
| Vehicle cost $K_cq_c$ | EV-location model; Bösch et al.'s autonomous-mobility cost classification; Fan et al.'s SAV planning; joint fleet/charging planning | Account for vehicle-related costs over the same evaluation period; distinguish fixed costs from costs incurred only when a trip is served |
| Extra unused-capacity penalty $c_c^+O_c^s$ | No direct supporting reference confirmed for this additional term | A study assumption reflecting an extra preference/loss; avoid counting costs already included in vehicle cost twice |
| Unmet-demand loss $c_c^-U_c^s$ | EV-location shortage structure, SAV service planning, and autonomous-mobility cost classification | Interpret as foregone contribution, not gross fare or an automatically observed cash payment |

**Takeaway:** structural literature support does not mean the cited papers supply the current dollar coefficients. In particular, a positive idle penalty needs a justification beyond ownership/holding costs already charged elsewhere.

## B. How the experimental parameters were set

B traces values using four labels: **O** = reported observation in a specific source/sample, **E** = published estimate, **D** = arithmetic derivation, **A** = designed synthetic assumption. A source-based scale reference does not turn a designed sensitivity range into an empirically validated range.

| Parameter | Baseline scale / derivation | Evidence and limitation |
|---|---|---|
| Productivity $\kappa_c$ | 24 trips/day ×365 = 8,760 trips/vehicle-year | D/O: rounded from reported Waymo trip/fleet totals. Both totals are lower-bound scale reports; realized throughput is not maximum service capacity |
| Reference market size $M_c$ | 38,527,207 annual TNC trips / 0.05 mode share = 770,544,140 opportunities/year | D/O: combines SFCTA and SFMTA references with imperfectly aligned periods/populations/trip units; not directly observed potential demand |
| Entry cost $F_c$ | (0.3M +2.5M facility-project estimates) ×1.25 = USD 3.5M | E/D/A: Austin project estimates plus an assumed 25% preparation allowance; not realized cross-city entry expenditures |
| Annual vehicle cost $K_c$ | USD 7,972/vehicle-year | D/O: selected AAA personal new-vehicle ownership-cost components used as a proxy; not measured robotaxi operating cost |
| Extra idle penalty $c_c^+$ | 0 in the baseline; positive levels in sensitivity | A: no additional idle loss in the reference case; positive penalties are preference assumptions |
| Unmet loss $c_c^-$ | USD 10/unserved trip | Quoted fares provide scale only. Retained fare 18 minus incremental cost 8 is an assumed illustrative calculation, not a margin estimated from the fare study |
| Fleet/city caps and probabilities | $Q=1,000$, city cap 500; scenario choice values specified by each experiment | A: resource limits and demand design are experimental inputs, not inferred optimal supply or calibrated choice shares |

### Why the sensitivity ranges matter

The document provides scale comparisons such as ±25% around productivity, market size, entry cost, and vehicle cost, plus alternative resource and penalty levels. The experiments use them to test whether mechanisms survive changes in assumptions, not to claim confidence intervals or actual city operating ranges.

The implemented annual experiment uses choice levels 0.002/0.005/0.01/0.02 to place demand near capacity; the parameter PDF contains different exploratory probability levels. Korean and English parameter PDFs also retain different probability ranges. Read the [annual experiment guide](../1.%20model/B.%20baseline_model/2%29%20numerical_experiments/large_case/README.md) for the actual implemented settings.

## How A and B should be used together

Use **A to justify what the model charges**, and **B to trace how an experimental coefficient was obtained**. Then check units, time period, source scope, double counting, and whether the value is observed, derived, or assumed. Together they support transparent synthetic validation; they do not complete real-city calibration.

The [model-structure guideline](%E2%80%BB%20translation/C.%20%EB%AA%A8%EB%8D%B8%20%EA%B5%AC%EC%A1%B0%20%EA%B0%80%EC%9D%B4%EB%93%9C%EB%9D%BC%EC%9D%B8.pdf) compares model families, while [papers](%E2%80%BB%20papers/README.md) explains their methodological foundations. The current revised ER-DRO model uses a different cost specification from the baseline; do not carry the baseline dollar objective over without checking that formulation.

[Project overview](../README.md)
