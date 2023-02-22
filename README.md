# 2022 UOS 빅데이터 알고리즘 경진대회 코드

## About

### Task

서울 4개 지역구의 2018~2021년도 데이터를 일자별 따릉이 사용량을 사용하여 2022년도의 지역구별 일자별 사용량을 예측

### Competition link

https://dacon.io/competitions/official/236029/overview/description


## Data

### Given Data

- 4개 지역구 별 따릉이 사용량
  - 데이터 예시

    ```csv
    일시,광진구,동대문구,성동구,중랑구
    20180101,0.592,0.368,0.58,0.162
    20180102,0.84,0.614,1.034,0.26
    20180103,0.828,0.576,0.952,0.288
    20180104,0.792,0.542,0.914,0.292
    20180105,0.818,0.602,0.994,0.308
    20180106,0.618,0.522,0.696,0.228
    20180107,0.598,0.478,0.606,0.238
    20180108,0.742,0.528,0.848,0.202
    20180109,0.652,0.488,0.838,0.206
    ...
    ```

  - 해당 데이터는 대회 사이트에서 참고해 주세요.

- 추가로 사용한 데이터
  - 공공데이터 특일정보
  - https://www.data.go.kr/data/15012690/openapi.do

### Data folder structure

```
data
|- holiday_test.csv
|- holiday_train.csv
|- sample_submission.csv
|- train.csv
```

## Method

- 공공데이터 API로 부터 휴일 정보를 불러와 csv형태로 저장
  - 기간별로 holiday_test.csv, holiday_train.csv로 저장
- preprocess 진행
  - 일시, 요일, 1년중 일수, 1년중 주차수, 연도, 월, 휴일 여부, 장마철 여부, 빨간날 여부 추가
  - (추가하였으나 이후에 빨간날 여부와 장마철 여부는 사용되지 않았음)
  - 4개 지역구 정보를 한번에 학습하기 위해 'loc' column에 각 지역구 정보를 입력
- GAM model 사용하여 학습
  - 'weekend', 'loc', 'vacation' 는 categorical data로 취급
  - 기타 variable들은 continuous data로 취급
  - 2018~2020 data로 학습 후 2021 data로 validation
  - submission은 2018~2021 data를 사용하여 학습

## Result

- 2018~2022 data로 학습 후 2021 데이터로 Validation 한 MAE
  - 2.07
- public score : 1.42315 / 9th
- private score : 1.81481 / 6th
- Awards : 3rd
