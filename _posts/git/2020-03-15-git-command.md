---
title: "git command"
layout: single
categories: [Git]
tags: [git]
toc: true #Table Of Contents 목차 보여줌
toc_label: "Contents" # toc 이름 정의
toc_icon: "list" #font Awesome아이콘으로 toc 아이콘 설정
toc_sticky: true # 스크롤 내릴때 같이 내려가는 목차
---

###### Configure setting
```
git config --global user.name "user_name"
git config --global user.email user_name@example.com
```

###### Create new local repository
```
git init
```

###### Check out repository
```
git clone [url or local_dir]
```

###### Add file
```
git add <file name>
``` 

###### Commit 
```
git commit -m "message"
```

###### Push
```
git push
```

###### Check status
```
git status
```

참고 : [Basic git commands](https://confluence.atlassian.com/bitbucketserver/basic-git-commands-776639767.html)