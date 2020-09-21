---
title: "Alsa - aplay, arecord"
layout: single
categories: [Linux]
tags: [linux, alsa]
toc: true #Table Of Contents 목차 보여줌
toc_label: "Contents" # toc 이름 정의
toc_icon: "list" #font Awesome아이콘으로 toc 아이콘 설정
toc_sticky: true # 스크롤 내릴때 같이 내려가는 목차
---

## Requirements
```bash
sudo apt-get install libasound2-dev
sudo apt-get install alsa-utils
```

 
## Check available device list
```bash
aplay -l
arecord -l
```

## Play sample file (.pcm)
```bash
aplay -D plughw:0,0 -t raw -c 1 -f S16_LE -r 44100 tmp.pcm
```
 - -D device : 'hw'나 'plughw'
       : 0,0 -> sound card number , device number
 - -t type
 - -c number of channels of file
 - -f format
 - -r sampling rate

## Play sample file(.wav)
```bash
aplay -D plughw:0,0 tmp.wav
```

## Record sample file(.wav)
```bash
arecord -D plughw:3,0 -f S16_LE -r 16000 -c 1 tmp.wav
```