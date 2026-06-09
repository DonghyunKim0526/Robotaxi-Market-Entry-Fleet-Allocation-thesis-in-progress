# Literature Review

어느 도시에 robotaxi를 배치할 수 있는가”는 수요가 큰 도시를 고르는 문제가 아니라, 먼저 법·허가와 ODD 적합성으로 도시를 거른 뒤 그 내부에서 수요 앵커가 강한 도시를 고르는 순차 필터 문제.(도시 (i)에 대해 법적으로 서비스가 허용되고, ODD 안에서 운영 가능한 시간·공간 비중이 충분, 그 안에서 관측 가능한 수요 앵커가 강한 도시를 선택하는 문제.

**1. NHTSA는 Level 4 자동화가 “limited service areas”에서만 동작한다고 설명, Waymo도 현재 서비스를 도시 전체가 아니라 이름이 명시된 서비스 구역 단위로 운영** 
-> [https://www.nhtsa.gov/laws-regulations/standing-general-order-crash-reporting]
Automated driving systems, still in development, encompass SAE Levels 3 through 5. In its mature state, a vehicle equipped with ADS aims to perform the entire dynamic driving task on a sustained basis within a defined operational design domain without driver involvement. 
-> 웨이모 근거 필요

**2. 도시 선정을 위한 가장 방어적인 공공데이터 변수군은 다음이다. 
수요 측면 : 인구·고용 밀도, 토지이용 혼합·walkability, 무차량 가구 비중, 소득, 공항 승객 규모, 대중교통 접근성
운영 측면 : 법·허가 상태, 도로유형/고속도로 비중, 교차로 밀도, 날씨·침수·극한기상 노출이 핵심**

-> Loa, P., Lee, Y. & Circella, G. Just another ride-hailing? examining the determinants of robotaxi demand in San Francisco. Transportation (2026). https://doi.org/10.1007/s11116-026-10751-9



고용밀도, 일자리 접근성, income, 무차량 가구 비
->https://arxiv.org/pdf/2406.11590 abstract 부분
Demographic factors, including population size and crime rate, emerge as the primary determinants positively influencing ride-sharing demand. Higher income levels, increased numbers of economically active citizens, and higher proportions of car-free households are associated with increased demand. Public transit availability and walkability also play significant roles in ride-sharing patterns in Chicago.  (ridesharing 연구임. 조심)

토지이용 혼합, walkability, 교차로 밀도, 공항 승객규
-> https://arxiv.org/pdf/2209.07980
the importance of built environment varies across spatial contexts, and it collectively contributes the largest importance in predicting ridesourcing demand for airport trips.”
“Ridesourcing demand is usually most responsive to the built environment changes for downtown trips, followed by neighborhood trips and airport trips. airport trips를 별도 spatial context로 다루며 built environment의 설명력이 특히 크다고 보고한다. (ridesharing 연구임. 조심)

대중교통 접근성. ridehailing과의 경쟁관계
->https://arxiv.org/abs/2104.04208
여섯 도시 Uber 데이터 분석은 public transport가 경쟁적일수록 ride-hailing demand share가 낮다고 보고했고, Chicago rail disruption 연구는 disruption 시 ridesourcing가 gap-filling capacity를 제공한다고 보고했다. Detroit/Ypsilanti MOD 선호 연구는 inferior transit services 지역에서 MOD 선호가 더 높다고 보고했다. 공개 학술 버전 기준


무엇이 ridesharing이랑 robotaxi의 수요를 가르는거지?


**3. 확률제약은 “수요가 랜덤”이기 때문만이 아니라, 날씨·침수·공사구간·리콜/서비스 중단 때문에 실제 투입 가능 fleet capacity 자체가 랜덤하게 줄어들기 때문에 필요**
-> https://www.reuters.com/legal/litigation/waymo-recall-nearly-3800-robotaxis-over-self-driving-software-issue-2026-05-12/

**robotaxi 현황
현재 확인되는 미국의 상용·공개 robotaxi 서비스는 여전히 지리적으로 제한된 metro/geofence 모델이다. Waymo Help는 샌프란시스코 베이 지역, 피닉스, 로스앤젤레스, 마이애미, 내슈빌, 올랜도, 달라스, 휴스턴, 샌안토니오를 직접 서비스 도시로 제시하고, 오스틴과 애틀랜타는 Uber를 통해 이용 가능하다고 명시한다. Zoox 역시 라스베이거스 공개 서비스와 샌프란시스코 제한적 탑승, 그리고 오스틴·마이애미 확장을 발표한 상태다. 이는 “전국 어디든 배치”가 아니라 “허가와 ODD 안에서 도시별로 선택적 배치”가 현재 산업의 실증적 형태임을 보여준다**













## Structure

- `meeting notes/`: notes in meetings.
- `papers/`: Literature review based on the references shared after my first meeting with Professor Siqian Shen.
  
## Main Topics

- Optimization under uncertainty
- Distributionally robust optimization
- Contextual stochastic optimization
- Multi-sourced data and information fusion
- Data-driven decision-making for logistics and resource allocation
