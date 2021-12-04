# Dacon_Solar_power_prediction
DACON 동서발전 태양광 발전량 예측 AI 경진대회 (public 33등/236팀)

<img src="https://user-images.githubusercontent.com/87663692/144705172-40f3873e-5116-4c47-9cee-3b4b9acc3bfb.png"
     width="200" height="300"/>

## 0. Notion 주소

notion 링크: https://steadfast-quill-cde.notion.site/5312820d84134cb5a2815ff7af9ffe5b

## 1. 주제

[https://dacon.io/competitions/official/235720/overview/description](https://dacon.io/competitions/official/235720/overview/description)

⇒ **동서발전 태양광 발전량 예측 AI 경진대회**

: 태양광 발전은 매일 기상 상황과 계절에 따른 일사량의 영향을 받습니다.
  이에 대한 예측이 가능하다면 보다 원활한 전력 수급 계획이 가능합니다.

**인공지능 기반 태양광 발전량 예측 모델**을 만드는 것이 목적인 대회였습니다.

## 2. 평가

- 심사 기준 : NMAE-10(Normalized Mean Absolute Error)

- Public 평가 : 학습용 제공 데이터를 이용하여 미래 한 달간 발전량 예측 후 평가
- Private 평가 : 대회 종료 시점부터 30일간 실제 발전량을 하루씩 평가

## 3. 데이터

- 내부데이터: 
site_info.csv (발전소 정보) : 발전소 발전용량(MW), 주소, 설치각, 입사각, 위도, 경도
energy.csv (발전소별 발전량) : 당진수상/당진자재창고/당진/울산 태양광 발전량. 1시간 단위 계량
(2018/03/01 00:00~2021/01/31 23:00)
dangjin_fcst_data.csv (당진지역 발전소 동네 예보) : 온도, 습도, 풍속, 풍향, 하늘상태(1,2,3,4)
(2018/03/01 00:00~2021/03/01 23:00)
dangjin_obs_data.csv (당진지역 발전소 기상 관측 자료) : 일시, 기온, 풍속, 풍향, 습도, 전운량(10분위)
(2018/03/01 00:00~2021/01/31 23:00)
ulsan_fcst_data.csv (울산지역 발전소 동네 예보) : 온도, 습도, 풍속, 풍향, 하늘상태(1,2,3,4)
(2018/03/01 00:00~2021/03/01 23:00)
ulsan_obs_data.csv (울산지역 발전소 기상 관측 자료) : 일시, 기온, 풍속, 풍향, 습도, 전운량(10분위)
(2018/03/01 00:00~2021/01/31 23:00)

- 외부데이터: 미세먼지, 이슬점 (2018/03/01 00:00~2021/01/31 23:00)
출처: 기상자료개방포털 (종관기상관측), - 에어코리아

## 4. 데이터 전처리

- NA 데이터 전처리: MICE, PPCA

- Forecast 보간 (cubic interpolation):
forecast data에서 예보 target time 3시간 간격으로 주어져 있어, cubic interpolation 해주었습니다.

- 파생변수 생성:

(i) 시간에 따른 천구상의 태양 좌표 변수 생성
<- day of year, 시간, 위도, 경도만 있으면 시간에 따른 천구상의 태양 좌표를 구해줄 수 있습니다.

(ii) WindSpeed(m/s)와 WindDirection(degree) 벡터 변환
<- 각도는 0과 360이 이어져야 하므로, 벡터 변환해주었습니다.

(iii) forecast data에 존재하지 않는 이슬점 변수 생성
<- 온도(Temperature), 상대습도(Humidity)을 이용해 생성
<- 추후 feature selection을 통해 다중공선성이 생기는 변수 제거

(iiii) Hour, day of year sin/cos 주기성 설정
<- 데이터를 그대로 사용할 경우, 날씨가 변하는 오후 24시와 오전 한 시/년도가 변하는 365일에서 1일 사이 급격한 변화가 발생합니다.
<- 이를 smooth하게 표현하기 위해 sin,cos으로 변환하여 주기서을 갖도록 설정해주었습니다.

(iiiii) observe data의 feature에 대한 3,6,12,24시간 단위 이동평균(MA) 변수 생성

## 5. 모델

LSTM 모델의 경우, 시간적 상관성과 기상 요인과의 상관성으로 인한 발전량 예측의 어려움을 해결할 수 있지만 결과가 비교적 좋지 않았습니다.
Sarimax(Sarima+exogeneous variable) 모델의 경우, trend에 대하여 ARIMA를 수행하고, 계절성에 대해서 추가적으로 ARIMA를 수행하는 모델입니다. 시계열 데이터에 적합한 모델이기에 사용해보았지만, 시간이 매우 많이 걸리며 그에 비해 결과가 좋지 않았습니다.
결론적으로 저희 팀은 LightGBM 모델과 grid_search로 best parameter를 찾아 사용했습니다.

## 6. 결과

Public 평가에서 총 240팀 중 35등을 기록했습니다.
<img src="https://user-images.githubusercontent.com/87663692/144706538-0d40efe0-537f-47c3-84d4-8e24c55dc237.png"
     width="550" height="300"/>
