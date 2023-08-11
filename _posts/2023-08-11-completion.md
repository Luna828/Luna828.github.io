---
title: "[iOS] Closure, Completion Handler, @escaping 알아보기"
layout: single
categories: iOS
tag: [swift, TIL, WIL]
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

즉, 쉽게 말하자면

비동기작업할 때, 작업의 완료를 기다리지 않고 다음 코드를 실행하는 동안, 작업이 완료가 되면 `completion` 클로저를 호출하여 작업의 결과를 전달

< completion 클로저 사용하는 경우 >

* 네트워크 요청 결과를 받아온 후 해당 결과 처리 경우
* 이미지를 다운로드 한 후 다운로드 완료 여부 처리
* 파일 작업이 완료된 후 파일 경로나 성공 여부 처리

-> 이런 경우 `completion`을 사용하여 작업 결과를 캡쳐하고 처리 ( 작업을 보다 효율적이게 다룰 수 있음)

```swift
func asyncAdd(a: Int, b: Int, completion: @escaping (Int) -> Void) {
  sleep(2) // 2초간 대기
  let result = a + b //result 값 캡쳐
      
  // 작업이 완료되면 completion handler 호출
  DispatchQueue.main.async {
    completion(result)
  }
}
 
// 비동기 작업 실행
asyncAdd(a:3, b:5) { result in 
  print(result)
}
```

위는 간단한 비동기 작업 실행 예제이다. 

밑의 코드는 TMDB의 Json 형식의 데이터를 디코딩하여 가져온 ImageUrl에서 이미지를 다운로드하여 `imageView`에 표시 또는 Error 처리를 하는 방식   

* 밑의 코드는 Json 디코딩은 아님 주의 *

```swift
func downloadImage(from urlString: String, completion: @escaping (UIImage?) -> Void) {
        guard let url = URL(string: urlString) else {
            completion(nil)
            return
        }
        
        URLSession.shared.dataTask(with: url) { data, response, error in
            guard let data = data, error == nil else {
                completion(nil)
                return
            }
            let image = UIImage(data: data)
            completion(image)
        }.resume()
    }
```
`downloadImage(from:completion:)`  함수는 주어진 URL로부터 이미지 데이터를 비동기적으로 다운로드하고, 다운로드 된 데이터를 UIImage 객체로 변환하여 Completion Handler를 통해 전달합니다.

```swift

// 원래 사용한 내 코드
APIManager.downloadImage(from: "\(IMG_URL)\(data.posterPath)"){ image in
  //
  DispatchQueue.main.async {
      cell.ImageView.image = image ?? UIImage(systemName: "house")
      cell.movieTitle.text = data.title
      cell.voteAverage.text = String(data.average)
  }
}
================================================================================
// 위의 비동기 함수를 사용하여 이미지 다운로드하는 방법의 쉬운 예시

downloadImage(from: "https://naver.com/image.jpg"){ image in 
  DispatherQueue.main.async {
    if let downloadedImage = image {
      imageView.image = downloadedImage
    } else {
      print("이미지 다운로드 실패")
    }
  }
}

```

## @escaping은 왜쓸까?

@escaping 속성은 클로저가 함수 외부에서 호출 될 수 있을 때 사용하는 것이다!

특히, 비동기 작업을 다룰 때 클로저는 함수가 끝나고 나서도 호출 될 수 있다. 

이 때 클로저를 함수 외부에서 호출 가능한 상태를 유지해야 함으로 @escaping을 사용

```swift

func fetchData(completion: @escaping ([String]?) -> Void) {
    // 네트워크 요청 등의 비동기 작업 수행
    // 작업이 완료되면 completion 클로저 호출
    let result = ["아바타", "짱구", "스파이더맨"]
    completion(result)
}


  // 비동기 작업 완료 후 결과 처리
  // 이 클로저는 fetchData 함수 외부에서 호출되므로 @escaping 필요
fetchData { result in
  if let movieNames = result {
    print(movieNames)
  } else {
    print("ERROR")
  }
}
print("Fetching data.. 데이터 패치중..."

```
비동기 작업이 진행되는 동안 데이터 패치중.. 메세지가 콘솔창에 출력되며, 작업이 완료되면 movieNames를 반환하거나 에러를 반환한다.








