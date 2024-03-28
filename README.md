# Hotel Booking Demand

## 프로젝트 개요
### 대회 소개
본 대회는 Kaggle에서 진행한 Community Competitions 대회로, 호텔 예약 데이터셋을 바탕으로 고객의 예약 취소 여부를 예측하는 대회다.

## 프로젝트 수행 과정
### Data Description
- 데이터셋에서 각 feature가 나타내는 정보를 파악하기 위해 Data Description을 작성하였다.
- 대회 페이지에 작성된 Data Description은 러시아어로 작성되있어, 이를 번역 및 검색한 내용을 토대로 Data Description을 작성하였다.
  
### EDA
- 데이터셋에서 고객의 예약 취소 분포를 확인한 결과, 다음과 같이 불균형한 분포를 보였다.<br>
![distribution_of_label](https://github.com/rlarlgh96/hotel-booking-demand/assets/121072239/00685821-372b-469f-8355-451d57d1434b)
- 데이터셋의 feature들을 데이터 값과 유형에 따라 다음과 같이 분류하였다.
  
  - 수치형 특성(numeric feature)
    - 연속형 데이터(continuous data)
    - 이산형 데이터(discrete data)

  - 범주형 특성(categorical feature)
    - 이진 데이터(binary data)
    - 순서형 데이터(ordinal data)
    - 명목형 데이터(nominal data)

- 예약 취소 여부에 따라 각 feature의 분포를 시각화하여, 어떤 feature가 고객의 예약 취소에 영향을 미치는지를 파악하였다.

  - 연속형 데이터의 경우, 예약 취소 여부에 따른 데이터의 분포 차이(평균, 분산, 사분위수)를 비교하였다.<br>
  ![distribution_of_continous_data](https://github.com/rlarlgh96/hotel-booking-demand/assets/121072239/7e50c6d9-203c-4353-8bec-ad16361820ee)
  - 이산형 데이터의 경우, 예약 취소 여부에 따른 데이터의 분포 차이(평균, 신뢰구간)를 비교하였다.<br>
  ![distribution_of_discrete_data](https://github.com/rlarlgh96/hotel-booking-demand/assets/121072239/9cdee033-dcbc-4084-a99e-c4bf64cc4697)
  - 이진 데이터의 경우, feature 값에 따라 예약 취소 분포를 시각화하여 기존의 분포와의 차이를 비교하였다.<br>
  ![distribution_of_binary_data](https://github.com/rlarlgh96/hotel-booking-demand/assets/121072239/867941c6-3348-4040-aa8a-31f2ebb2a494)
  - 순서형 데이터와 명목형 데이터의 경우, feature 값에 따른 예약 취소율을 그래프로 나타내어 전체 데이터셋의 예약 취소율과의 차이를 비교하였다.<br>
  ![distribution_of_nominal_data](https://github.com/rlarlgh96/hotel-booking-demand/assets/121072239/f20add64-7eee-4a90-9752-12b76294f25a)
  
### Data Preprocessing
- EDA를 통해 다음 feature들이 고객의 예약 취소 여부에 영향을 미칠 가능성이 있다고 판단하였다.
  
  - hotel, lead_time, meal, market_segment, deposit_type, customer_type, total_of_special_requests

- lead_time과 total_of_special_requests feature는 이상치를 제거하기 위해 별도로 Data Cleaning을 진행하였다.
- 또, 원본 데이터에서 유용한 feature를 추출하기 위해 Feature Extraction을 진행하였다. 추출한 feature는 다음과 같다.

  - is_checked_out: 고객이 실제로 체크아웃을 했는지를 나타내는 데이터, arrival_date와 reservation_status_date로부터 추출
  - room_changed: 예약한 객실과 실제 배정받은 객실이 일치하는지를 나타내는 데이터, reserved_room_type와 assigned_room_type로부터 추출

- 위 feature들로 상관관계 히트맵을 그려 상관 관계 분석을 실시하였다. target feature와의 상관계수가 0.1이 넘는 feature들을 최종적으로 모델에 사용할 feature로 선택하였다.
- 선택된 feature들의 상관관계 히트맵은 다음과 같다.<br>
![correlation_heatmap](https://github.com/rlarlgh96/hotel-booking-demand/assets/121072239/34ae04a6-4a81-4b97-a5d3-86ff4d466ef9)

### Modeling
- 문제를 풀기위해 다음 세 가지 방법으로 모델링을 진행하였다.
  
  - Rule-based Classification(RBC): is_checked_out이 0이면 취소, 1이면 아닌 것으로 예측
  - Logistic Regression(LR): 선택된 feature 갯수에 따라 input 노드가 8개인 선형 레이어 구조로 모델 설계
  - Multilayer Perceptron(MLP): Logistic Regression의 모델 구조에서 노드가 4개인 중간 레이어 추가

## 프로젝트 수행 결과
- 평가 데이터셋에서 각 모델의 성능은 다음과 같다.

  | model | score |
  |--------|--------|
  | RBC | 0.99744 |
  | LR | 0.99234 |
  | MLP | 0.98027 |
  
- 리더보드 제출 결과, 302팀 중 3등을 기록했다.(2024년 2월 28일 기준)<br>
<img width="980" alt="leaderboard" src="https://github.com/rlarlgh96/hotel-booking-demand/assets/121072239/ef8182d9-a05f-47cb-9746-3bcf6bd19ff5">

## 참고문헌
- 신백균. (2022). *Must Have 머신러닝·딥러닝 문제해결 전략*. 골든래빗(주).
