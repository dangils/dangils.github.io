---
title: "[AI] Time Series 개요"
date: "2023-01-05 21:27:02"
categories: [AI,Time Series]
tags: [AI,Time Series]


---

## Time Series Forecasting model

> Time SERIES Forecasting model의 분류
> Univariate : 하나의 특성을 사용
> Multivariate: 여러 개의 특성 사용

------------

## TIme series Forecasting model 알고리즘

- Autoregressive (AR) : 시계열의 이전 값과 이후 값 사이 어느 정도의 상관 관계(자기 상관)가 있을 때 사용
- Autoregressive Integrated Moving Average (ARIMA) : 시계열 예측에 있어 가장 많이 사용되는 모델, 시계열 데이터 내 자체적으로 lagged (지연된) 데이터를 생성해 이를 예측한 오류를 기반으로 계산하는 방식
- Seasonal Autoregressive Integrated Moving Average (SARIMA) : ARIMA에 계절성을 확장시킨 모델
- Exponential Smoothing (ES) : 추세 또는 계절성을 사용한 univariate 데이터 예측 방법
- XGBoost
- Prophet
- LSTM (Deep Learning)

-----------

## 시계열 패턴

**추세(trend)**
- 데이터가 장기적으로 증가하거나 감소할때, 추세(trend)가 존재
- 추세가 반드시 선형적일 필요는 없음

**계절성(seasonality)**
- 해마다 어떤 특정한 때나 1주일마다 특정 요일에 나타나는 것 같은 패턴
- 계절성은 빈도의 형태로 나타나며, 그 빈도는 항상 일정

**주기성(cycle)**
- 고정된 빈도가 아닌 형태로 증가나 감소하는 모습을 보일 때
- 경제 상황 때문에 발생, 흔히 “경기 순환(business cycle)”과 관련



-----------

### 시계열 예제

![](https://otexts.com/fppkr/fpp_files/figure-html/fourexamples-1.png)

1) 미국 단독 주택 거래량:
    - 약 6~10년의 몇몇 강한 주기적 패턴이 보이지만 분명한 추세가 있지는 않음

2) 미국 재무부 증권(treasury bill) 계약:
   - 계절성은 없지만 하향하는 추세 있음

3) 호주 분기별 전력 생산:
   - 강한 계절성과 함께 강한 증가 추세

4) 구글 주식 종가 기준 일별 변동
   - 추세나 계절성, 주기적인 행동이 없음, 무작위적인 요동


-----------


## 시계열 예측 딥러닝 모델에 영향을 주는 요소
1) 데이터 수 : 늘릴수록 성능 향상

2) history data : 이전 시점을 얼마만큼 사용하는지에 따라 성능 변화 없음 (어차피 자체적으로 현재 시점에서 가까운 데이터에 대한 가중치를 높게 설정하기 때문)

3) future data : 현재 시점을 기준으로 더 멀수록 예측의 정확도가 낮아짐

4) 이상치 필터링 : 이상치를 필터링할수록 성능이 눈에 띄게 성능이 향상됨 but 이상치를 필터링할 경우, 학습한 데이터 중 이상치가 없어 이상에 대한 예측이 불가함, 이상치가 축적되었을 때 학습


-------------

## 시계열 예측 Process
1) 데이터셋 탐색
    - 기본 데이터 탐색적 분석
2) 모델 학습을 위한 데이터 전처리
    - 지도학습용 데이터로 변환(multi step)
    - 구축된 데이터를 학습용, 검증용, 시험용 데이터로 분리
    - 데이터 스케일링
3) 모델 학습 및 예측값 확인




