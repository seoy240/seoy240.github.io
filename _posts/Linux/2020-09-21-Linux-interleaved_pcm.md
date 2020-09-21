---
title: "pcm 저장 방식(interleaved / non-interleaved)"
layout: single
categories: [Linux]
tags: [linux, alsa]
toc: true #Table Of Contents 목차 보여줌
toc_label: "Contents" # toc 이름 정의
toc_icon: "list" #font Awesome아이콘으로 toc 아이콘 설정
toc_sticky: true # 스크롤 내릴때 같이 내려가는 목차
---


### 스테레오 채널 저장시 저장 순서

- Interleaved : LRLRLR 
- Non-interleaved : LLLRRR

한 채널당 ( bitPerSample/8 ) byte 씩 저장됨

따라서 스테레오 채널에서 한 샘플당 버퍼의 크기(byte) = bitsPerSample / 8 * (Nchannel) byte


```
(ex) channels = 2  bit depth = 16 인 경우 interleaved 저장 방식
 _________________________________________________
|    Sample 0   |    Sample 1   |     Sample 2    |  Frames
| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 | 11 |  Bytes
|  Left | Right | Left  | Right | Left  |  Right  |  Channels
 -------------------------------------------------
```

[참고]<https://github.com/melchor629/node-flac-bindings/wiki/interleaved-pcm-audio>