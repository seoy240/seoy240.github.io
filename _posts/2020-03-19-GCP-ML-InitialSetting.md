---
title: "Machine learning with GCP - Initial setting"
layout: single
categories: [GCP]
tags: [GCP, ML]
toc: true #Table Of Contents 목차 보여줌
toc_label: "Contents" # toc 이름 정의
toc_icon: "list" #font Awesome아이콘으로 toc 아이콘 설정
toc_sticky: true # 스크롤 내릴때 같이 내려가는 목차
---

### Create Storage Bucket
Navigation Menu > Storage > Create bucket 
Bucket 이름 설정후 create

### Launch AI Platform Notebokks
Navigation Menu > AI Platform > Notebooks
New instance 생성 
Open JupyterLab 실행
terminal 실행하여 원하는 git clone 가능

### Set Bucket / Project / Region
BUCKET이름은 Navigation Menu > Storage > Browser에서 확인할 수 있다.
PROJECT 와 BUCKET은 모두 unique한 이름이여야 하며, 두개 다 동일 이름으로 설정하면 편리하다.
```
BUCKET = 'qwiklabs-gcp-02-dbbfecfc31a1'
PROJECT = 'qwiklabs-gcp-02-dbbfecfc31a1'
REGION = 'us-east1'
```
위의 설정은 python에서 적용가능하도록 설정한것이므로 bash에서도 적용할 수 있도록 아래와 같이 입력한다.
```
import os
os.environ['BUCKET'] = BUCKET
os.environ['PROJECT'] = PROJECT
os.environ['REGION'] = REGION
```
Bucket이 생성되지 않은 경우 bucket을 생성하도록 한다.
```
%%bash
if ! gsutil ls | grep -q gs://${BUCKET}/; then
  gsutil mb -l ${REGION} gs://${BUCKET}
fi
```

