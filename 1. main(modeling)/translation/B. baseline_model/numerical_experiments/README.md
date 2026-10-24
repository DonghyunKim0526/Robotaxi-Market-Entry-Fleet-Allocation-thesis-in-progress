# Baseline 수치실험 한글 자료

## 실험이 검증하는 것

1. 수식과 MILP 구현의 일치: 목적값 재계산, 정수성, 차량 상한, 수요·용량 균형을 검사합니다.
2. 경계 조건: 차량·수요 0, 매우 큰 진입비, 수요와 용량의 일치에서 예상대로 동작하는지 확인합니다.
3. 민감도와 불확실성: 한 번에 한 입력을 바꾸고 동률 해·평균수요 결정·시나리오 표본의 영향을 비교합니다.

| 구분 | Small case | Large case |
|---|---|---|
| 후보 도시 / 시나리오 | 3 / 10 | 3 / 10 |
| 전체 차량 | 4 | 1,000 |
| 대표 최적 배치 | (0,2,2), 유일해 | (132,368,500), 72개 동률 |
| 목적값 | 858 USD | 166,263,859 USD |
| 처리율 | 30.0% | 34.93% |
| 독립 검증 | 60개 진입·배치 조합 전수계산 | 정수 동적계획법 |

![작은 사례의 도시별 처리·미충족과 배치별 목적값: (0,2,2)가 858로 최적입니다.](smallcase/figures/01_baseline.png)

작은 사례의 도시별 처리·미충족과 배치별 목적값: (0,2,2)가 858로 최적입니다.

세 도시로 나누면 처리량은 조금 증가하지만 추가 진입비를 회수하지 못합니다. 한글 PDF는 small case를 설명하며, large case의 상세 보고서는 영문 폴더에 있습니다. 현재 `smallcase` 폴더에는 두 한글 코드가 함께 배치되어 있습니다. 모든 수치는 합성 실험 결과입니다.

## 코드와 Colab 실행

- **[baseline_largecase(한글).ipynb](smallcase/baseline_largecase%28%ED%95%9C%EA%B8%80%29.ipynb)** · [Colab](https://colab.research.google.com/drive/1YsArFdKTv3LFnlhcAC__o0PlrfRD-eEx) — 연간 입력 MILP·독립 DP, 72개 동률 해, 공통·도시별 민감도, 시나리오 표본실험과 CSV·그래프 출력.
- **[baseline_smallcase(한글).ipynb](smallcase/baseline_smallcase%28%ED%95%9C%EA%B8%80%29.ipynb)** · [Colab](https://colab.research.google.com/drive/1VT-cDsVp_YqmNhzPgUUk2LuJHBpc97tK) — 작은 사례 MILP·60개 전수계산 대조, E1–E8, 민감도·평균수요 비교 및 그래프 출력.

Colab은 접근 권한이 있는 Drive 원본을 엽니다. GitHub 파일은 저장된 사본이며 자동 동기화되지 않습니다.

## 관련 폴더

- [smallcase](smallcase/README.md)


---

[상위 안내](../README.md) · [전체 연구 안내](../../../../README.md)
