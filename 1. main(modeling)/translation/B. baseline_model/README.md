# Baseline 모형 한글 자료

## Baseline의 구조

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

$y_c$는 진입 여부, $q_c$는 차량 대수입니다. 초기 진입비 $F$, 연간 차량비 $K$, 유휴 페널티 $c^+$와 미충족 공헌이익 손실 $c^-$를 최소화합니다. 진입하지 않은 도시에는 차량을 배치할 수 없고, 도시별 상한과 전체 차량 한도가 적용됩니다.

## 수요와 부족의 구분

- $M$은 전체 잠재 이동 기회, $p$는 용량 부족을 적용하기 전 로봇택시를 선택할 확률입니다.
- $M(1-p)$는 처음부터 로봇택시를 선택하지 않은 수요이며, 로봇택시를 원했지만 못 탄 $U$와 다릅니다.
- 한글 문서에는 $M_c^s,p_c^{R,s}$ 및 부족 후 전환의 이전 표기가 있습니다. 현재 실행 baseline은 고정 $M_c$와 외생적 $p_c^s$를 사용하므로 최신 영문 식도 확인하세요.

## 수치실험의 핵심 결과

Small case는 $(0,2,2)$, 목적값 858이며 가능한 60개 결정을 전수계산한 결과와 일치합니다. 추가 도시의 처리 이익 8이 진입비 20보다 작아 B·C 집중이 유리합니다. Large case의 대표해는 $(132,368,500)$이며 72개 동률 배치가 있습니다. 두 한글 노트북은 현재 지정된 `numerical_experiments/smallcase`에 함께 있습니다.

## 문서와 핵심 내용

- **[baseline(main).pdf](baseline%28main%29.pdf)** — M·p·로봇택시 선택수요와 부족 후 전환을 설명한 한글 모형입니다. 이전 표기가 있어 현재 실행식은 최신 영문 baseline과 함께 확인합니다.


## 관련 폴더

- [numerical_experiments](numerical_experiments/README.md)


---

[상위 안내](../README.md) · [전체 연구 안내](../../../README.md)
