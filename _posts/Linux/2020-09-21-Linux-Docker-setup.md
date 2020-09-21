---
title: "Docker 환경구성"
layout: single
categories: [Linux]
tags: [linux, docker]
toc: true #Table Of Contents 목차 보여줌
toc_label: "Contents" # toc 이름 정의
toc_icon: "list" #font Awesome아이콘으로 toc 아이콘 설정
toc_sticky: true # 스크롤 내릴때 같이 내려가는 목차
---

### deepo 이미지 사용
```bash
docker pull ufoym/deepo
```

### 로컬pc 그래픽을 도커에서 사용할 수 있도록 추가
도커에서 pyqt같은 gui사용할 수 있도록 하기 위함
```bash
xhost +local:docker
```

### 도커 컨테이너 생성
```bash
docker run -it \
--gpus all \
--device=/dev/snd \
-h name_tmp --name name_tmp \
-v local_dir:docker_dir \
-e DISPLAY=$DISPLAY \
-v /tmp/.X11-unix:/tmp/.X11-unix \
ufoym/deepo
```
- -it :터미널 입력을 위한 옵션
- --gpus all: local pc의 gpu 전부 사용
- --device=/dev/snd: local pc의 sound device 사용
- -h name_tmp --name name_tmp: 컨테이너의 hostname = name_tmp, container name = name_tmp 으로 설정
- -v local_dir:docker_dir: local pc의 local_dir와 docker의 docker_dir의 데이터 볼륨 공유
- -e DISPLAY=$DISPLAY: 디스플레이 설정을 위한 옵션
- -v /tmp/.X11-unix:/tmp/.X11-unix: 디스플레이 설정을 위한 옵션

### sndfile 오류 발생시
```
apt-get update
apt-get install libsndfile1
```
- 참고 <https://stackoverflow.com/questions/44910504/trying-to-install-libsndfile-on-ubuntu-16>