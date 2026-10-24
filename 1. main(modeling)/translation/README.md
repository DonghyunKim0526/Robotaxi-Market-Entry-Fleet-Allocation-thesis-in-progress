# 모형 한글 자료

## 모형별 핵심

| 자료 | 핵심 내용 | 확인할 결과·차이 |
|---|---|---|
| 초기 모형 | newsvendor → 비용 최소화 → 이익 최대화 → 복수 페널티 | 수요·처리량·손실의 정의와 비용 중복 계산 방지 |
| Baseline | 고정 $M$과 외생적 $p$로 $D=Mp$ 생성, 진입·차량 배치 후 유휴·부족 비용 계산 | small case $(0,2,2)$, 목적값 858; 한글 large-case 코드도 수치실험 폴더에 있음 |
| ER-DRO | 도시 특성에 로짓 회귀 잔차를 붙여 시나리오 생성, 평균 대신 CVaR로 평가 | 평균비용 증가와 꼬리비용 감소의 교환관계 |

```math
D_c^s=M_cp_c^s,\quad T_c^s=\min(D_c^s,\kappa_cq_c),\quad
O_c^s=(\kappa_cq_c-D_c^s)_+,\quad U_c^s=(D_c^s-\kappa_cq_c)_+.
```

$y,q$는 시나리오 공통 결정이고 $O,U$는 시나리오별 결과입니다. Baseline은 진입비·차량비·기대 페널티를 합산하지만 revised ER-DRO는 별도 차량비 항을 두지 않으므로 목적값을 직접 비교하지 않습니다.

한글 baseline 문서에는 시나리오별 시장규모·미충족 후 전환 등 이전 표기가 남아 있습니다. 실행 코드와 현재 정의를 맞출 때는 최신 영문 baseline도 함께 확인하세요. 본 실험은 합성 설정이며 실제 도시의 수요·최적 배치를 추정한 결과가 아닙니다.

## 관련 폴더

- [A. former_model ideas](A.%20former_model%20ideas/README.md)
- [B. baseline_model](B.%20baseline_model/README.md)
- [C. ER-DRO_model](C.%20ER-DRO_model/README.md)


---

[상위 안내](../README.md) · [전체 연구 안내](../../README.md)
