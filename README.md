# Dacon_Solar_power_prediction
DACON 동서발전 태양광 발전량 예측 AI 경진대회 (public 33등/236팀)

## 1. 주제

[https://dacon.io/competitions/official/235720/overview/description](https://dacon.io/competitions/official/235720/overview/description)

⇒ **동서발전 태양광 발전량 예측 AI 경진대회**

: 태양광 발전은 매일 기상 상황과 계절에 따른 일사량의 영향을 받습니다.

이에 대한 예측이 가능하다면 보다 원활한 전력 수급 계획이 가능합니다.

**인공지능 기반 태양광 발전량 예측 모델**을 만드는 것이 목적인 대회였습니다.

## 2. 평가

- 심사 기준 : NMAE-10(Normalized Mean Absolute Error)

```python
import pandas as pd
import numpy as np

def sola_nmae(answer_df, submission_df):
    submission = submission_df[submission_df['time'].isin(answer_df['time'])]
    submission.index = range(submission.shape[0])

    # 시간대별 총 발전량
    sum_submission = submission.iloc[:,1:].sum(axis=1)
    sum_answer = answer_df.iloc[:,1:].sum(axis=1)

    # 발전소 발전용량
    capacity = {
        'dangjin_floating':1000, # 당진수상태양광 발전용량
        'dangjin_warehouse':700, # 당진자재창고태양광 발전용량
        'dangjin':1000, # 당진태양광 발전용량
        'ulsan':500 # 울산태양광 발전용량
    }

    # 총 발전용량
    total_capacity = np.sum(list(capacity.values())) 

    # 총 발전용량 절대오차
    absolute_error = (sum_answer - sum_submission).abs()

    # 발전용량으로 정규화
    absolute_error /= total_capacity

    # 총 발전용량의 10% 이상 발전한 데이터 인덱스 추출
    target_idx = sum_answer[sum_answer>=total_capacity0.1].index

    # NMAE(%)
    nmae = 100 * absolute_error[target_idx].mean()
    return nmae
```

- Public 평가 : 학습용 제공 데이터를 이용하여 미래 한 달간 발전량 예측 후 평가
- Private 평가 : 대회 종료 시점부터 30일간 실제 발전량을 하루씩 평가


