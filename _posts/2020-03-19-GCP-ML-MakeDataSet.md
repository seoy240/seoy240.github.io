---
title: "Machine learning with GCP - Make data set"
layout: single
categories: [GCP]
tags: [GCP, ML]
toc: true #Table Of Contents 목차 보여줌
toc_label: "Contents" # toc 이름 정의
toc_icon: "list" #font Awesome아이콘으로 toc 아이콘 설정
toc_sticky: true # 스크롤 내릴때 같이 내려가는 목차
---

### Load Data set
구글 클라우드의 public data를 불러온다.
```
# Create SQL query using natality data after the year 2000
from google.cloud import bigquery
query = """
SELECT
  weight_pounds,
  is_male,
  mother_age,
  plurality,
  gestation_weeks,
  FARM_FINGERPRINT(CONCAT(CAST(YEAR AS STRING), CAST(month AS STRING))) AS hashmonth
FROM
  publicdata.samples.natality
WHERE year > 2000
"""
```
- SELECT : 지정하는 정보의 값을 가져온다. 
- WHERE : 2000년 이후 출산한 경우의 정보만 가져온다.
- FARM_FINGERPRINT : YEAR,month 정보를 HASH값 (hashmonth)으로 만든다.
* YEAR,month 정보를 HASH값으로 만들었기 대문에 같은 연도, 같은 달에 태어난 아기는 같은 HASH 값을 가지게 된다.


### Create Data set
불러온 데이터 `query` 를 TRAINING / EVALUATION SET로 나눈다.
- 조건: 약12,000 training 샘플 / 약 3000 evaluation 샘플
- 당연히 고르게 분포되어 있어야 하며 겹치지 않아야 한다.
```
sampling_query = "SELECT COUNT(weight_pounds) FROM (" + query + ") WHERE MOD(ABS(hashmonth), 10) < 8 AND RAND() < 0.0004"
print(sampling_query)
```

hashmonth를 통해 겹치지 않는 데이터셋을 만들수 있다.
이 경우에는 hashmonth를 10을 나눈 나머지를 통해 구분하였는데, training/evaluation 샘플수의 비율이 4:1 정도이므로 
`MOD(ABS(hashmonth), 10) < 8`  인 경우 training, `MOD(ABS(hashmonth), 10) >= 8` 인 경우 evaluation으로 분리 할 수 있다.
또한 `RAND() < 0.0004`를 통해 데이터셋 별로 전체적인 샘플 수를 조절하였다.
이 경우 RAND() < 0.0004 로 설정할 경우 10713개 정도로 나왔는데 따라서 training set으로 조건에 부합한다.
마찬가지로 샘플의 수를 2배로 늘리고 싶다면 RAND() < 0.0008 로 설정하면 될 것이다.

- 정리 
* `MOD(ABS(), )`  를 통해 각 데이터 셋의 비율 조절
* `RAND()` 를 통해 데이터 셋 전체의 샘플 수 조절

### Create data set in detail
null 값을 갖는 경우를 제외하고 데이터를 불러온다.
```
# Create SQL query using natality data after the year 2000
from google.cloud import bigquery
sampling_query = """
SELECT * FROM(
SELECT
  weight_pounds,
  is_male,
  mother_age,
  plurality,
  gestation_weeks,
  FARM_FINGERPRINT(CONCAT(CAST(YEAR AS STRING), CAST(month AS STRING))) AS hashmonth
FROM
  publicdata.samples.natality
WHERE year > 2000 AND is_male IS NOT null AND plurality is NOT null AND weight_pounds is NOT null
) WHERE MOD(ABS(hashmonth), 10) < 8 AND RAND() < 0.0004
"""
```
각 값을 문자열로 바꾸거나 내가 원하는 값으로 변경할수도 있다.
```
df2['is_male'] = 'Unknown'
df2['plurality'] = 'Single' if ... else 'Multiple'
df2.head()
```

### Save data set
```
traindf.to_csv('train.csv', index=False, header=False)
evaldf.to_csv('eval.csv', index=False, header=False)
```

### bash로 저장한 data set 정보 확인
- wc: word count
- head/tail : panda 함수와 비숫한 동작
```
%%bash
wc -l *.csv
head *.csv
tail *.csv
```