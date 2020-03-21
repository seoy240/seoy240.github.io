---
title: "Machine learning with GCP - Preprocessing Using Cloud Dataflow"
layout: single
categories: [GCP]
tags: [GCP, ML]
toc: true #Table Of Contents 목차 보여줌
toc_label: "Contents" # toc 이름 정의
toc_icon: "list" #font Awesome아이콘으로 toc 아이콘 설정
toc_sticky: true # 스크롤 내릴때 같이 내려가는 목차
---
Apache Beam 과 Cloud dataflow를 이용한 데이터 전처리 방법
- Pandas를 이용한 전처리도 가능하지만 elastic한 처리를 위해서는 Apachem beam을 사용하는 것이 좋다.
- Apache Beam : elastic data processing pipeline을 생성하기 위해 사용
	- 동일한 pipeline 코드를 이용하여 streaming, batch process 모두 가능하다.
- Cloud dataflow : apache beam을 적용

Local에서 작은 데이터로 동작을 확인한 후 cloud에서 전체 data로 돌리는 것이 좋다.
- Process in local
```
python ./etl.py
```
- Process in cloud : speciy cloud parameters
	- cloud에서 실행하기 위해 runner을 실행해야 한다.
```
python ./etl.py \
	--project=$PROJECT \
	--job_name=myjob \
	--staging_location:gs://$BUCKET/staging/ \
	--temp_location:gs://$BUCKET/staging/ \
	--runner=DataFlowRunner
```

### Apache beam 설치 
```
pip install --user apache-beam[gcp]
```

### Preprocessing using Apache beam and cloud dataflow

코드 : <https://github.com/GoogleCloudPlatform/training-data-analyst/blob/master/courses/machine_learning/deepdive/06_structured/labs/4_preproc.ipynb>

위의 코드를 실행후 GCP web console의 Dataflow section에 가면 dataflow와 작업이 실행되고 있는 것을 확인할 수 있다.
![image](/assets/images/GCP/img_1.JPG)
