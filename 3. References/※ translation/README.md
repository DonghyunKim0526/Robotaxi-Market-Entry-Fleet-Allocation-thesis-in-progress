# 참고자료·파라미터 근거: 한글

## 자료별 핵심

| 문서 | 핵심 내용 | 연구에서의 역할 |
|---|---|---|
| 비용항목 선정 근거 | 진입비·차량비·미충족 공헌이익 손실의 구조적 근거; 추가 유휴 페널티는 연구 가정 | 어떤 항을 목적함수에 넣는지 설명 |
| 파라미터 근거 | 관측 O / 발표 추정 E / 환산 D / 합성 가정 A 구분 | 수치의 출처와 실험값의 한계를 추적 |
| 모델 구조 가이드라인 | Baseline → ER-SAA → ER-DRO → 결정의존 확장 비교 | Context, 강건성, 결정의존성을 구분 |
| 메모 | 종속변수 정의, 자료 부족, 변수 선택·잔차·외삽 검토 과제 | 확정 결론이 아닌 연구 검토 기록 |

## 수식으로 보는 차이

```math
\text{Baseline: }\min_{y,q}\sum_c(F_cy_c+K_cq_c)+\frac1N\sum_s H(q,D^s)
```

```math
\text{Contextual DRO: }\min_{y,q}\text{first-stage cost}
+\sup_{P\in\mathcal U(x)}\mathbb E_P[H(q,D(x,\varepsilon))].
```

Contextual은 도시 특성 $x$에 따라 시나리오가 달라지는 것이며, 결정의존은 수요 자체가 $D(x,q,\varepsilon)$처럼 차량 배치 등에 반응하는 것입니다. 현재 ER-DRO 코드는 전자만 포함합니다. Revised 모형은 별도 $Kq$를 생략해 baseline과 비용 정의가 다릅니다.

파라미터 기준값은 $\kappa=8,760$, reference $M=770,544,140$, $F=3.5$M, $K=7,972$, $c^+=0,c^-=10$입니다. 이는 서로 다른 출처의 규모 참고·환산·가정을 결합한 합성 설정입니다. 한글·영문 파라미터 PDF와 실제 annual 코드의 $p$ 범위는 일치하지 않으므로 실행 결과는 코드의 실제 입력을 기준으로 읽으세요.

## 문서와 핵심 내용

- **[A. cost_selection_rationale(한글).pdf](A.%20cost_selection_rationale%28%ED%95%9C%EA%B8%80%29.pdf)** — 목적함수 항별 구조적 문헌 근거·비용 분류·연구 추가 가정을 구분합니다. 비용항의 근거와 실제 계수 추정을 혼동하지 않습니다.
- **[B. parameter_rationale_baseline(한글).pdf](B.%20parameter_rationale_baseline%28%ED%95%9C%EA%B8%80%29.pdf)** — 관측·발표 추정·환산·가정을 구분하고 연간 κ·M·F·K와 페널티의 설정 이유 및 적용 한계를 설명합니다.
- **[메모.pdf](%EB%A9%94%EB%AA%A8.pdf)** — M/p 관측·회귀 종속변수·잔차·외삽·자료 부족 등 연구 검토 과제를 기록합니다. 현재 확정된 모형 사양은 아닙니다.
- **[모델 구조 가이드라인.pdf](%EB%AA%A8%EB%8D%B8%20%EA%B5%AC%EC%A1%B0%20%EA%B0%80%EC%9D%B4%EB%93%9C%EB%9D%BC%EC%9D%B8.pdf)** — Baseline, contextual ER-SAA, ER-DRO, 결정의존 모형의 수식과 구현 차이를 비교합니다.


---

[상위 안내](../README.md) · [전체 연구 안내](../../README.md)
