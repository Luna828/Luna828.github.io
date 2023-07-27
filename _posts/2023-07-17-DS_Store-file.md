---
title: ".DS_Store 파일 및 .gitignore 처리"
layout: single
categories: swift
tag: [TIL, 스파르타코딩, 내일배움캠프, 7기, iOS, swift]
toc: true
---

맥북에서 자꾸 git에 커밋할 때마다 생기는 .DS_Store 파일때문에 골치 아파서 구글링.. 시작

# .DS_Store 란?

* DS_Store 는 Desktop Services Store 약자로, 애플에서 정의한 파일 포맷
* `Mac OS 시스템`이 `Finder`로 접근할 때 자동으로 생기는 파일로, 해당 폴더에 대한 메타데이터를 저장
* 맥 os 에서 생성 및 사용되지만 git에 올릴 때 같이 공유되는 경우가 생김
* 해당 폴더에 대한 `메타데이터`의 저장으로 이 파일을 통해 `보안 침해`가 발생 할 수 있음

# .DS_Store -> gitignore 하기

깃헙에서 레포를 팔 때, gitignore 생성 후 꼭 맨 밑에 저렇게 넣어줍니다.. ㅎ

```
.DS_Store 
```

# Github에 올라갔다면?

```
//터미널에서

//파일 확인하기
ls -a | grep .DS_Store

//파일 제거
rm .DS_Store


```


