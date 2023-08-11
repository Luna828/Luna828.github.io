---
title: "[iOS] Completion Handler 알아보기"
layout: single
categories: iOS
tag: [swift, storyboard, TIL, WIL]
toc: true
---

스터디 팀원들과 TMDB를 사용하여 api 통신 공부를 하면서 알게 된 Completion 에 대해 알아보기 위한 글이다!

## 클로저 & 후행 클로저

먼저 completion을 사용하기 전에 클로저에 대해서 알아보도록 하겠습니당!

클로저는 변수나 상수로 `저장` 하거나 `전달` 할 수 있으며, 함수처럼 `매개변수와 반화 값`을 가질 수 있다.
클로저는 `1급 객체`

```swift
// 클로저~
func car(completion: () -> ()) {
  completion()
}

// completion 매개변수 타입은 매개변수는 없고 리턴 타입도 없음!

// 클로저 사용방식!
car {
  print("K9")
}
```

```swift
// 기본 클로저 예시
let add: (Int, Int) -> Int = { (a, b) in
    return a + b
}

let result = add(2, 3)
print(result) // 출력: 5
```

후행 클로저는 함수의 매개변수 목록 뒤에 작성되는 클로저
```swift
//후행 클로저
func calculate(a: Int, b: Int, operation: (Int, Int) -> Int) -> Int {
    return operation(a, b)
}

// 두 정수와 클로저를 받아 

let result = calculate(a: 5, b: 3) { (a, b) in
    return a - b
}

print(result) // 출력: 2

```
클로저를 사용하는 이유 : 
  1. 코드 재사용: 기존 함수를 수정하지 않고 다양한 동작 가능, 재사용성 증가
  2. 코드 경량화: 작은 코드 블록을 표한하는 데 더 적게 사용 가능
  4. 비동기 작업 처리: 비동기 작업 결과를 클로저 내부에서 처리하거나, 비동기 작업 완료시 사용
  5. 콜백 기능: 비동기 작업에서 완료시 호출되는 콜백 함수로 사용 가능

## Completion Handler

Completion Handler는 비동기적인 작업을 수행한 후 결과를 전달하거나 처리 

```swift

```



