---
title: "[swift] 에러처리(Error Handling)"
layout: single
categories: swift
tag: swift
toc: true
---

# 에러 처리
* 프로그램에서 에러가 발생한 상황에 대응하고 처리하는 과정입니다
* Swift는 런타임 에러가 발생한 경우, 이를 지원하는 클래스 제공
* Error 프로토콜을 채택하여 사용자 정의 에러를 정의하여 사용할 수 있다.

---

### throws, do-catch 

* throw 와 throws
  - `throws` : 리턴 값을 반환하기 전에 오류가 발생하면 에러 객체 반환
  - `throws` : 오류가 발생할 가능성이 이쓴ㄴ 메소드 제목 옆에 쓰임
  - `throw` : 오류가 발생할 구간에서 사용

* throw로 던진 에러를 do-catch문 처리

```swift
//표현식
func canThrowErrors() throws -> String

//enum 으로 Errorcase 정의
enum VendingMachineError: Error {
    case invalidSelection
    case insufficientFunds(coinsNeeded: Int)
    case outOfStock
}

//ErrorCase 사용법
class VendingMachine {
    var inventory = [
        "Candy Bar": Item(price: 12, count: 7),
        "Chips": Item(price: 10, count: 4),
        "Pretzels": Item(price: 7, count: 11)
    ]
    var coinsDeposited = 0

    func vend(itemNamed name: String) throws { // 👀
        guard let item = inventory[name] else {
            throw VendingMachineError.invalidSelection
        }

        guard item.count > 0 else { 
            throw VendingMachineError.outOfStock // 👀
        }

        guard item.price <= coinsDeposited else {
            throw VendingMachineError.insufficientFunds(coinsNeeded: item.price - coinsDeposited) // 👀
        }

        coinsDeposited -= item.price

        var newItem = item
        newItem.count -= 1
        inventory[name] = newItem

        print("Dispensing \(name)")
    }
}

```

### try? 와 try!
* try? 
  - do-catch 없이 사용가능
  - 에러 발생시 nil반환
  - 에러발생X 리턴 값 옵셔널
* try!
  - 에러 발생시 앱 강제종료
  - 반환 값 - 옵셔널 언래핑된 값
  - 오류가 발생하지 않는다는 보장 아래 사용 권장

* 예시 (다음 기회에..)
---

에러의 예외처리에는 여러가지 방법들이있다.

아직까지는 강의에 나온 정도로만 이해하고있고 

구글에서 다른 방법들을 찾아본 결과 아직 어떤식으로 사용하는지 감은 오지 않는다... 

밑에 링크에 `라이노의 개발블로그`에 가보면 여러가지의 에러 핸들링 예제에 대해 나와있어 차근차근 배워가면 좋을 것같다고 생각하고있다

Link: [Error_Handling](https://rhino-developer.tistory.com/entry/Swift-ErrorHandling) 


[TO BE CONTINUE ....]
