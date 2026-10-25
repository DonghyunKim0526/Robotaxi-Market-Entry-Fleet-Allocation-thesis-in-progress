# 기본 모형

## 폴더·파일 안내

| 폴더·문서 | 내용 |
|---|---|
| [기본 모형 정식화](baseline%28main%29.pdf) | 수요·비용·진입·차량·유휴·부족의 정의 |
| [수치실험](numerical_experiments/README.md) | 작은 사례와 연간 큰 사례의 목적·설정·검증 |
| [작은 사례 보고서·코드](numerical_experiments/smallcase/README.md) | 전수검증·경계검사·전환점·불확실성 비교 |
| [영문 큰 사례 보고서·코드](../../B.%20baseline_model/2%29%20numerical_experiments/large_case/README.md) | 규모 근거·독립 DP·민감도·동률·표본 안정성 |
| [이전 정식화 보관본](../../B.%20baseline_model/3%29%20revision_history/) | 과거 PDF의 모형 정의 비교 |

한글 코드는 기존 지정대로 수치실험의 같은 폴더에 함께 보관합니다.

### 실험 실행

| 코드 | 수행 내용 | 실행 |
|---|---|---|
| [작은 사례 한글 코드](numerical_experiments/smallcase/baseline_smallcase%28%ED%95%9C%EA%B8%80%29.ipynb) | MILP·60개 전수계산·경계·민감도·평균수요 비교 | [Colab](https://colab.research.google.com/drive/1VT-cDsVp_YqmNhzPgUUk2LuJHBpc97tK) |
| [연간 큰 사례 한글 코드](numerical_experiments/smallcase/baseline_largecase%28%ED%95%9C%EA%B8%80%29.ipynb) | MILP·정확 DP·도시별 민감도·동률·표본·CSV | [Colab](https://colab.research.google.com/drive/1YsArFdKTv3LFnlhcAC__o0PlrfRD-eEx) |

Colab은 접근 권한이 있는 Drive 원본을 엽니다. GitHub 노트북은 저장된 사본이며 자동으로 동기화되지 않습니다.

## 기본 모형이 표현하는 것

수요 관측 전에 도시 진입과 정수 차량을 정합니다. 수요는 고정 시장규모×외생 선택확률이며 모든 시나리오에 같은 배치를 적용합니다.

```math
\min_{y,q,O,U}\sum_cF_cy_c+\sum_cK_cq_c+
\frac1{|S|}\sum_{s,c}(c_c^+O_c^s+c_c^-U_c^s)
```

$y,q$는 진입·차량, $F,K$는 초기 진입·연간 차량비입니다. 유휴와 부족은 용량·수요의 차이로 계산합니다. 미진입 시 차량 0, 도시별·전체 차량 상한, 용량 균형이 적용됩니다. 고정비와 기대 서비스 손실을 절충하며 상세 기호는 [모형 문서](baseline%28main%29.pdf)에서 확인합니다. 한글 원문 일부는 이전 표기이므로 최신 영문 정의도 함께 봅니다.

## 수치실험: 목적과 설계

모형의 구현과 경제적 작동 원리가 일치하는지 점검합니다. 최종 배치 자체보다 왜 그 결과가 나오는지가 핵심입니다.

| 점검 | 작은 사례 | 연간 큰 사례 |
|---|---|---|
| 설정 목적 | 전수계산과 직접 해석 가능한 합성 정수 | 연간 규모·수요 민감도·동률·표본 점검 |
| 기본 세팅 | 도시 3·시나리오 10, 전체 4·도시 상한 2·생산성 10 | 도시 3·시나리오 10, 전체 1,000·도시 상한 500·생산성 8,760 |
| 독립 검증 | 60개 진입·배치 전수계산 | 정확 동적계획법과 목적값·제약 재계산 |
| 동작 분석 | 경계 8개·진입비·생산성·시장규모·유휴·변동성 | 경계 8개·공통/도시별 민감도·전체 동률 해 |
| 불확실성 | 평균수요의 모든 동률 결정을 원래 분포로 평가 | 같은 평가와 50·100·500개×5개 시드 표본실험 |

작은 사례는 검증용 합성값입니다. 큰 사례는 공개 규모 참고·환산·가정을 결합했으며 실제 도시 보정이 아닙니다.

### 모형 점검에서 확인한 점

- **구현:** 보고된 MILP와 독립 기준 풀이가 일치하며 경계에서 제약의 역할을 확인합니다.
- **진입 경제성:** 작은 사례에서 추가 서비스 공헌 8보다 추가 진입비 20이 커 집중 배치가 유리합니다. 공통 진입비 8에서 전환합니다.
- **용량·비용:** 다른 제약이 허용할 때만 차량 증가가 유리합니다. 배치가 같아도 비용·동률 해는 달라질 수 있습니다.
- **불확실성·동률:** 평균만으로 시나리오별 유휴·부족을 알 수 없으며 연간 사례는 동률 72개입니다.

![진입비에 따른 배치·서비스·비용 분해·미진입 대비 개선](numerical_experiments/smallcase/figures/06_F_zoom.png)

![시나리오 표본수에 따른 평균수요·공통 분포 추가비용](../../B.%20baseline_model/2%29%20numerical_experiments/large_case/figures/annual/17_sampling.png)

첫 그림은 서비스 가치와 고정비의 비교를, 둘째는 원래 분포에서 표본으로 선택한 결정의 품질을 보여줍니다. 50개 표본은 추가비용 최대 약 1.73M, 500개는 5개 시드 모두 0입니다. 이는 가정 분포에서의 안정성이지 실수요 검증이 아닙니다. 음영은 동률 범위로 신뢰구간이 아닙니다.

재현 기준은 작은 사례 (0,2,2)·858, 큰 사례 대표 (132,368,500)·약 166.264M입니다. 상세 해석은 사례별 안내를 봅니다.

### 보고서와 실행 코드

| 사례 | 설계·해석 | 코드 | 실행 |
|---|---|---|---|
| 작은 사례 | [안내](numerical_experiments/smallcase/README.md) · [보고서](numerical_experiments/smallcase/small_case%28%ED%95%9C%EA%B8%80%29.pdf) | [한글 코드](numerical_experiments/smallcase/baseline_smallcase%28%ED%95%9C%EA%B8%80%29.ipynb) | [Colab](https://colab.research.google.com/drive/1VT-cDsVp_YqmNhzPgUUk2LuJHBpc97tK) |
| 연간 큰 사례 | [영문 안내](../../B.%20baseline_model/2%29%20numerical_experiments/large_case/README.md) · [영문 보고서](../../B.%20baseline_model/2%29%20numerical_experiments/large_case/large_case.pdf) | [한글 코드](numerical_experiments/smallcase/baseline_largecase%28%ED%95%9C%EA%B8%80%29.ipynb) | [Colab](https://colab.research.google.com/drive/1YsArFdKTv3LFnlhcAC__o0PlrfRD-eEx) |

입력→독립 검증→경계→민감도·불확실성 순서로 모두 실행합니다. Colab은 접근 권한이 있는 Drive 원본을 엽니다. GitHub 노트북은 저장된 사본이며 자동으로 동기화되지 않습니다.

## 한계와 ER-DRO로의 확장

기본 모형은 선택 시나리오를 입력으로 받으므로 도시 특성에서 수요를 학습하거나 시나리오 확률의 오지정을 보호하지 않습니다. 합성 검증은 실시장 예측 검증이 아닙니다. [ER-DRO](../C.%20ER-DRO_model/README.md)는 로짓·잔차로 도시별 수요를 만들고 CVaR로 평균/꼬리비용을 비교합니다. 현재도 수요는 외생적이며 결정의존·실제자료 검증은 이후 과제입니다.

---

[상위 안내](../README.md) · [전체 연구 안내](../../../README.md)
