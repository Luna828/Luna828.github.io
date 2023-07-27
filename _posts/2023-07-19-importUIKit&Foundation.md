---
title: "[swift] UIKit & Foundation"
layout: single
categories: swift
tag: [swift, iOS, TIL]
toc: true
---

# [swift] Import UIKit 와 Foundation

iOS 개발 공부를 시작하면서 import Foundation 과 import UIKit 이라는 것을 자주 보게되서 알아봐야지 ~ 하다가! 

오늘 같은 팀원 분들 중 한분이 물어봐주셔서 같이 찾아본 겸 정리해보는 시간을 가지게되었다ㅎㅎ 

## UIKit

* UIKit은 그래픽과 사용자 중심 사용자 인터페이스 구조 및 관리하는 인터페이스이다
* 애니매이션, 문서, 그리기 , 현재 장치의 정보, 텍스트, 접근성 등을 관리하는 것

참고로, UIKit > Foundation이 포함 되어져있어서 UIKit이 더 큰 개념이라고 생각하면된다 
```swift
import UIKit
import Foundation
```
두개 다 임포트 해줄 필요가없다 !!!

![UIKit](https://github.com/Luna828/luna828.github.io/assets/93186591/52281d44-35f5-4b2c-927f-f277dc26f0cb)

UIKit 안에 들어가 보면 위 사진처럼 임포트 문들이 엄청 많다...

## Foundation

공식문서에 따르면 밑의 사진과 같이 어떤 곳에 필요한지 정확하게 나와있습니다!

[iOS 공식문서 Foundation](https://developer.apple.com/documentation/foundation#//apple_ref/doc/uid/20001091)

<img width="744" alt="스크린샷 2023-07-19 오후 9 09 38" src="https://github.com/Luna828/luna828.github.io/assets/93186591/2d223d6a-5963-417f-90c0-f17380957854">

* 앱개발의 기초적인것들 (자료구조, 시간, 데이터 포맷, filter와sorting 등)
* App 서포트
  - Task Management
  - Resources
  - Notifications
  - App Extension Support
  - Error and Exceptions
* 파일과 데이터 구조
* 네트워킹

그 외에 등등이 있는데 대부분 기초적으로 앱을 개발하는데 쓰이는 모든 것들이 들어가 있다고 생각하면 되는 것 같다.








