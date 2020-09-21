---
title: "Docker 명령어"
layout: single
categories: [Linux]
tags: [linux, docker]
toc: true #Table Of Contents 목차 보여줌
toc_label: "Contents" # toc 이름 정의
toc_icon: "list" #font Awesome아이콘으로 toc 아이콘 설정
toc_sticky: true # 스크롤 내릴때 같이 내려가는 목차
---

```bash
#container 확인
docker ps -a

#start container
docker start (container name)

#container 접속 - 다중 접속 가능
docker exec -it (container name)  bash
```