# Robotaxi-Market-Entry-Fleet-Allocation (thesis in progress)

## Research question and model

Which candidate cities should a robotaxi operator enter, and how many vehicles should it allocate before demand is known? Entry is binary, fleet allocation is integer, and each demand scenario produces unused capacity or unmet demand.

```math
\min_{y,q,O,U}\;\sum_c F_cy_c+\sum_c K_cq_c+
\frac{1}{|S|}\sum_{s,c}(c_c^+O_c^s+c_c^-U_c^s)
```

```math
D_c^s=M_cp_c^s,\qquad
\kappa_cq_c-D_c^s=O_c^s-U_c^s
```

```math
0\le q_c\le\bar q_cy_c,\quad \sum_cq_c\le Q,\quad
y_c\in\{0,1\},\ q_c\in\mathbb Z_{\ge0},\ O_c^s,U_c^s\ge0.
```

Here $y_c$ selects a city, $q_c$ allocates vehicles, $M_c$ is potential annual trip opportunities, and $p_c^s$ is robotaxi choice probability. $F_c$ is entry cost, $K_c$ is annual vehicle cost, and $c_c^+,c_c^-$ price surplus capacity and unmet demand. All scenarios share the same entry and fleet decisions.

## What the research establishes so far

| Component | Main finding | Where to inspect it |
|---|---|---|
| Baseline verification | Small-case optimum $(0,2,2)$, cost 858; matches all 60 feasible entry/fleet pairs | [Small-case results and code](1.%20main%28modeling%29/B.%20baseline_model/2%29%20numerical_experiments/small_case/README.md) |
| Annual synthetic experiment | Representative optimum $(132,368,500)$; 72 tied allocations; service rate 34.93% | [Annual-case results and code](1.%20main%28modeling%29/B.%20baseline_model/2%29%20numerical_experiments/large_case/README.md) |
| Contextual ER-DRO | Residual scenarios connect city characteristics to demand; CVaR trades mean cost for tail protection | [ER-DRO formulation and experiments](1.%20main%28modeling%29/C.%20ER-DRO_model/README.md) |
| Demand inputs | Construct fixed $M_c$ from trip-generation rates and population; estimate $p$ using comparable city context | [M and p input selection](2.%20driving%20factors/C.%20Selection/README.md) |

## Representative result

![Annual baseline: representative fleet, served versus unmet demand, and objective improvement over no entry.](1.%20main%28modeling%29/B.%20baseline_model/2%29%20numerical_experiments/large_case/figures/annual/02_baseline.png)

Annual baseline: representative fleet, served versus unmet demand, and objective improvement over no entry.

The annual instance enters all three cities and uses 1,000 vehicles. The representative allocation is one of 72 optima: A gets 132 vehicles while B and C share 868. This is a synthetic model experiment, not a calibrated recommendation for those cities.

## From the baseline to ER-DRO

Baseline experiments specify $p_c^s$ directly. ER-DRO instead fits logit-scale choice probabilities, adds empirical residuals to each candidate city's context, and minimizes a CVaR cost over those scenarios. At $\zeta=0$ it becomes ER-SAA; larger $\zeta$ emphasizes costly scenarios. The present notebook has exogenous context and **no decision-dependent demand**.

The revised ER-DRO formulation drops the separate vehicle-cost term used in the baseline. Its cost coefficients and objective values therefore should not be compared directly with baseline costs. Real-data demand calibration and decision-dependent extensions remain research tasks.

## Code and Colab launch

- **[baseline_largecase.ipynb](1.%20main%28modeling%29/B.%20baseline_model/2%29%20numerical_experiments/large_case/baseline_largecase.ipynb)** · [Colab](https://colab.research.google.com/drive/1eLKtC6O0tr65SM1JkziHM24RaPbEDo3_) — Annual MILP + exact DP; tied optima, common/city sensitivity, mean-demand evaluation, and scenario sampling; exports CSVs and plots.
- **[baseline_smallcase.ipynb](1.%20main%28modeling%29/B.%20baseline_model/2%29%20numerical_experiments/small_case/baseline_smallcase.ipynb)** · [Colab](https://colab.research.google.com/drive/1xJvXZokBwrCa2vabDtKB1izIU3fAevtx) — Small MILP + 60-pair exhaustive reference; edge tests, sensitivity, and common-scenario mean-demand comparison.
- **[ER-DRO(non decision-dependent).ipynb](1.%20main%28modeling%29/C.%20ER-DRO_model/ER-DRO%28non%20decision-dependent%29.ipynb)** · [Colab](https://colab.research.google.com/drive/1dz5QtiAnYBBmKfDLi95xfjFirqg2fcAT) — Logit learning → residual scenarios → ER-SAA/ER-DRO/no-context decisions → independent OOS scoring; diagnostics, optional decomposition, and CSV exports.
- **[baseline_largecase(한글).ipynb](1.%20main%28modeling%29/translation/B.%20baseline_model/numerical_experiments/smallcase/baseline_largecase%28%ED%95%9C%EA%B8%80%29.ipynb)** · [Colab](https://colab.research.google.com/drive/1YsArFdKTv3LFnlhcAC__o0PlrfRD-eEx) — 연간 입력 MILP·독립 DP, 72개 동률 해, 공통·도시별 민감도, 시나리오 표본실험과 CSV·그래프 출력.
- **[baseline_smallcase(한글).ipynb](1.%20main%28modeling%29/translation/B.%20baseline_model/numerical_experiments/smallcase/baseline_smallcase%28%ED%95%9C%EA%B8%80%29.ipynb)** · [Colab](https://colab.research.google.com/drive/1VT-cDsVp_YqmNhzPgUUk2LuJHBpc97tK) — 작은 사례 MILP·60개 전수계산 대조, E1–E8, 민감도·평균수요 비교 및 그래프 출력.
- **[ER-DRO(non decision-dependent 한글).ipynb](1.%20main%28modeling%29/translation/C.%20ER-DRO_model/ER-DRO%28non%20decision-dependent%20%ED%95%9C%EA%B8%80%29.ipynb)** · [Colab](https://colab.research.google.com/drive/17iILpKgogewmOCaTxgyWJqE7_LOHQ_7o) — 로짓 학습→잔차 시나리오→ER-SAA/ER-DRO/no-context→독립 OOS 평가; 회귀 진단·선택 분해 비교·CSV·민감도 출력.

Colab opens the permission-controlled Drive original. The GitHub notebook is a saved snapshot; changes are not automatically synchronized.

## Related folders

- [1. main(modeling)](1.%20main%28modeling%29/README.md)
- [2. driving factors](2.%20driving%20factors/README.md)
- [3. References](3.%20References/README.md)
