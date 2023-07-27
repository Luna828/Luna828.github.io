---
title: "Swift 기초공부"
layout: single
categories: swift
tag: swift
toc: true
---

# Swift Study

## Swift 기초

이 자료는 boostcourse 의 무료강의를 보고 배운 것을 정리하려고 쓴 블로그 입니다!
Link: [boostcourse](https://www.boostcourse.org/mo122)

### 명명법

- Lower Camel Case: 함수, 메소드, variable, constant (goToHome)
- Upper Camel Case: type(class, struct, enum, extension)  (Person, Car, Week)
스위프트는 모든 대소문자를 구분한다고 합니다!

### Console log 남기기

- print("아빠") : 단순 문자열 출력
- dump("아빠") : 인스턴스의 자세한 설명(description 프로퍼티)까지 출력

### 문자열 보간법
- 프로그램 실행 중 문자열 내에 변수 또는 상수의 실질적인 값을 표현하기 위해서 사용합니다!

```swift
import Swift
let name: String = "LUNA"

print("안녕하세요! 저는 \(name) 입니다") 
//출력: 안녕하세요! 저는 LUNA 입니다
dump(name) 
//출력 "LUNA"
```

```swift
class Person {
    var name: String = "LUNA"
    var age: Int = 24
}

let Luna: Person = Person()
print(Luna)
print("\n##################\n")
dump(Luna)

//출력 값:

//main.Person
//##################
//main.Person #0
//  - name: "LUNA"
//  - age: 24
```
### 상수와 변수 선언

* let: 상수 선언 키워드
* var: 변수 선언 키워드

```swift
// 상수와 변수 선언
let 상수이름: 타입 = 값
var 변수이름: 타입 = 값

// 값의 타입이 명확하다면 타입 생략 가능
let 상수이름 = 값
var 변수이름 = 값

// 상수와 변수 활용
let constant: String = "차후에 변경이 불가능한 상수 let"
var variable: String = "차후에 변경이 가능한 변수 var"

variable = "변수는 이렇게 차후에 다른 값을 할당할 수 있지만"
// constant = "상수는 차후에 값을 변경할 수 없습니다" // 오류발생
```

constant는 아래와 같은 에러가 난다.
`Cannot assign to value: 'constant' is a 'let' constant` 

```swift
let sum: Int
let inputA: Int = 100
let inputB: Int = 200

// 선언 후 첫 할당
sum = inputA + inputB

// sum = 1 // 그 이후에는 다시 값을 바꿀 수 없습니다, 오류발생

// 변수도 물론 차후에 할당하는 것이 가능합니다
var nickName: String

nickName = "yagom"

// 변수는 차후에 다시 다른 값을 할당해도 문제가 없지요
nickName = "LUNA"
```

### Any, AnyObject, nill

기본 데이터 타입은 아니지만 데이터 타입 위치에서 수행하는 Any, AnyObject, 없음 = nill

* Any - Swift의 모든 타입을 지칭하는 키워드
* AnyObject - 모든 클래스 타입을 지칭하는 프로토콜
* nil - '없음'을 의미하는 키워드

1. Any
```swift
var someAny: Any = 100
someAny = "LUNA"
someAny = 123.456

//Any는 어떤 타입도 수용이 가능합니다
```
2. AnyObject
```swift
class SomeClass {}
var someAnyObject: AnyObject = SomeClass()

// AnyObject는 클래스의 인스턴스만 수용 가능하기 때문에 클래스의 인스턴스가 아니면 할당할 수 없습니다.
someAnyObject = 123.12    // 컴파일 오류발생

```

3. nil
```swift
// someAny는 Any 타입이고, someAnyObject는 AnyObject 타입이기 때문에 nil을 할당할 수 없습니다.
var someAny: Any = 100
var someAnyObject: AnyObject = SomeClass()

// nil을 다루는 방법은 옵셔널 파트에서 다룹니다.
someAny = nil         // 컴파일 오류발생
someAnyObject = nil   // 컴파일 오류발생
```
nill은 그냥 없다 -> null, NULL, Null 과 유사하다


### 고차함수

고차함수란? : 다른함수를 전달인자로 받거나 함수실행의 결과를 함수로 반환하는 함수

#### map
```swift
//for
let num = ["1","2","3","4","5"]
numberArray = []
for index in num {
  if let changeToInt = Int(index){
    numberArray.append(changeToInt)
  }
}

//map
let stringArray = ["1","2","3","4","5"]
numberArray = stringArray.map{Int($0)!}

//출처 : 스파르타 코딩 swift 문법강의
```

#### filter
기존 컨테이너 요소 중 조건에 만족하는 값에 대해 새로운 컨테이너를 만들어 반환 가능 
```swift
// for 문으로 구현
// numbers에서 짝수만 추출하기

let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9]
var evenNumbers: [Int] = []

for number in numbers {
    if number % 2 == 0 {
        evenNumbers.append(number)
    }
}

print(evenNumbers)
// [2, 4, 6, 8]

// filter로 구현
// numbers에서 짝수만 추출하기

let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9]
let evenNumbers = numbers.filter { $0 % 2 == 0 }

print(evenNumbers)
// [2, 4, 6, 8]

//출처 : 스파르타 코딩 swift 문법강의
```

#### reduce
기존의 컨테이너의 요소에 대해 정의한 클로저로 매핑한 결과를 새로운 컨테이너로 반환
```swift
// for 문으로 구현
// 각 요소의 합 구하기

let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
var sum = 0

for number in numbers {
    sum += number
}

print(sum)
// 55


// reduce로 구현
// 표현식1
// 각 요소의 합 구하기

let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
let sum = numbers.reduce(0, +)

print(sum)
// 55


//표현식2
// 각 요소의 합 구하기

let numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
let sum = numbers.reduce(0) { $0 + $1 }

print(sum)
// 55


//출처 : 스파르타 코딩 swift 문법강의
```

#### switch
```swift
let cookieCount = 62
let message: String
switch cookieCount {
case 0:
    message = "🍪 없음 🙅‍♂️"
case 1..<5:
    message = "🍪 아주 조금 있음"
case 5..<12:
    message = "🍪 조금 있음"
case 12..<100:
    message = "🍪 꽤 있음 🍪"
case 100..<1000:
    message = "🍪🍪 많음 🍪🍪"
default:
    message = "🍪🍪🍪엄청 많음🍪🍪🍪"
}
print(message)

//출처 : 스파르타 코딩 swift 문법강의
```

### 옵셔널 바인딩
* 옵셔널 바인딩은 옵셔널 값이 빈값인지 존재하는 지 검사한 후, 존재하는 경우 다른 변수에 대입시켜 바인딩함
* if let / if var, guard let/ guard var 을 써 옵셔널 값 -> 새로운 변수 바인딩
* if let : 코드 구현부 내에서만 상수 사용 가능 (지역변수)
* guard let : guard 조건을 통과한 상수를 guard문 밖에서 사용 가능 (전역변수)

#### 옵셔널 강제 언래핑 방법
```swift
let number = Int("42")!
// String값을 Int로 변환하는 함수는 return값으로 옵셔널 값을 반환합니다.
print(number)

//출처 : 스파르타 코딩 swift 문법강의
```
이와 같이 강제 언래핑을 한 옵셔널은 추천 XXXX

#### 옵셔널 체이닝
* 옵셔널을 연쇄적으로 사용하는 것
```swift
struct Person {
	var name: String
	var address: Address
}

struct Address {
	var city: String
	var street: String
	var detail: String
}

let sam: Person? = Person(name: "Sam", address: Address(city: "서울", street: "신논현로", detail: "100"))
print(sam.address.city) // 에러 🚨. 에러 메시지: Chain the optional using '?' to access member 'address' only for non-'nil' base values
sam?.address.city  // ✅

//출처 : 스파르타 코딩 swift 문법강의
``` 







### 컬렉션 타입

* Array: 순서가 있는 리스트 컬렉션
* Dictionary: '키' 와 '값' 으로 이루어진 컬렉션
* Set: 순서가 없고, 멤버가 유일한 컬렉션




