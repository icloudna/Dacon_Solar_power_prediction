# 데이터 소개

## site_info.csv _ 발전소 정보

Id : 사이트 식별자

Capacity : 발전소 발전용량(MW)

Address : 주소

InstallationAngle : 설치각(º)

IncidentAngle : 입사각(º)

Latitude : 위도

Longitude : 경도

## energy.csv _ 발전소별 발전량

time : 1시간 단위 계량된 시간 (ex-2018-03-01 1:00:00 => 2018-03-01 00:00:00 ~ 2018-03-01 1:00:00 1시간동안 발전량 계량)

dangjin_floating : 당진수상태양광 발전량(KW)

dangjin_warehouse : 당진자재창고태양광 발전량(KW)

dangjin : 당진태양광 발전량(KW)

ulsan : 울산태양광 발전량(KW)

## dangjin_fcst_data.csv _ 당진지역 발전소 동네 예보

Forecast time : 예보 발표 시점

forecast : 예보 시간 

(Forecast time:2018-03-01 11:00:00, forecast:4.0 → 2018-03-01 11:00:00에 발표한 2018-03-01 15:00:00 예보)

Temperature : 온도(℃)

Humidity : 습도(%)

WindSpeed : 풍속(m/s)

WindDirection : 풍향(º)

Cloud : 하늘상태(1-맑음, 2-구름보통, 3-구름많음, 4-흐림)

## dangjin_obs_data.csv _ 당진지역 발전소 인근 기상 관측 자료

지점 : 지점 코드
지점명 : 관측소 지점
일시 : 관측 시간
기온(°C) : 기온(°C)
풍속(m/s) : 풍속(m/s)
풍향(16방위) : 풍향(º)
습도(%) : 습도(%)
전운량(10분위) : 전운량(낮을 수록 구름이 적음)

## ulsan_fcst_data.csv _ 울산지역 발전소 동네 예보

Forecast time : 예보 발표 시점

forecast : 예보 시간 

(Forecast time:2018-03-01 11:00:00, forecast:4.0 → 2018-03-01 11:00:00에 발표한 2018-03-01 15:00:00 예보)

Temperature : 온도(℃)

Humidity : 습도(%)

WindSpeed : 풍속(m/s)

WindDirection : 풍향(º)

Cloud : 하늘상태(1-맑음, 2-구름보통, 3-구름많음, 4-흐림)

## ulsan_obs_data.csv _ 울산지역 발전소 인근 기상 관측 자료

지점 : 지점 코드

지점명 : 관측소 지점

일시 : 관측 시간

기온(°C) : 기온(°C)

풍속(m/s) : 풍속(m/s)

풍향(16방위) : 풍향(º)

습도(%) : 습도(%)

전운량(10분위) : 전운량(낮을 수록 구름이 적음)

## sample_submission.csv _ 예측한 발전량 제출 양식

public LB : 2021년 2월 예측

private LB : 2021년 6월 9일 ~ 2021년 7월 8일 30일간 예측, 평가기간 제출 가능, 예측 전날 선택된 제출물 평가

time : 지난 한시간동안 발전량 예측

dangjin_floating : 당진수상태양광 예측 발전량(KW)

dangjin_warehouse : 당진자재창고태양광 예측 발전량(KW)

ulsan : 울산태양광 예측 발전량(KW)
