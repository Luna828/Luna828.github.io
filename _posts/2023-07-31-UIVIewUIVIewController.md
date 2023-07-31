---
title: "[iOS] UIView 와 UIViewController"
layout: single
categories: iOS
tag: [swift, storyboard, TIL, WIL]
toc: true
---

# iOS의 UI 구성요소를 살펴보자

## UIView

* UI를 구성하는 객체
* 화면에 보이는 모든 요소들의 기본 클래스
* 모든 시각적 요소 (글자, 아이콘, 이미지) UIView의 하위 클래스 OR UIView를 상속받는 클래스

특징
* 위치나 크기 (`frame`, `bound`, `center`) 조정 가능
* 배경색 (`background`, `alpha`, `layer`) 변경 가능
* 애니메이션 효과 (`UIView.animate`, `UIViewPropertyAnimator`) 구현 가능
* `addSubview(_:)` 활용하여 superview, subview 형태로 계층적 구조화를 통해 내용 구성 가능
* Auto Layout 
* 스토리 보드의 기본적 구성요소

UIButton, UILabel, UIImageView, UIWebView, UIScrollView, UITableView 등등

```swift
// UIView 객체 생성
let myView = UIView(frame: CGRect(x: 0, y: 0, width: 100, height: 100))

// 뷰의 배경색상 지정
myView.backgroundColor = UIColor.red

// 뷰를 서브뷰로 추가 - 이것을 꼭 해줘야 실행했을 때 화면에 그려지는게 보여질 수 있음
self.view.addSubview(myView)

// 뷰의 위치 및 크기 변경
myView.frame = CGRect(x: 50, y: 50, width: 200, height: 200)
```


## UIViewController

iOS 생명주기와 연결되어져 있으며 아래 코드와 같이 사용됨

### 뷰의 상태 변화 감지 메소드
 * viewDidLoad()
  - 뷰 계층이 메모리에 로드된 직후 초기화 작업
  - 1회 호출, 재사용 불가 (뷰가 사라지지않는 이상)

* viewWillAppear
  - 뷰가 뷰 계층에 추가되고 화면이 표시되기 직전 호출 (필요한 데이터를 미리 부를 때 좋음)

* viewDidAppear
  - 뷰가 뷰 계층에 추가되어 화면이 표시되면 호출
  - 뷰를 보여줄 때 필요한 추가적인 작업 (사용자 입력같은 거)

* viewWillDisappear
  - 뷰가 뷰계층에서 사라지기 직전에 호출
  - 다른 화면 이동시, 필요한 작업

* viewDidDisappear
  - 뷰가 뷰 계층에서 사라진 후 호출
  - 뷰를 숨기는 것과 관련된 것
  
```swift
class MyViewController: UIViewController {
    override func viewDidLoad() {
        super.viewDidLoad()
        // 화면이 로드되었을 때 필요한 초기화 작업을 수행합니다.
    }
    
    override func viewWillAppear(_ animated: Bool) {
        super.viewWillAppear(animated)
        // 화면이 나타나기 전에 필요한 데이터를 설정하거나 기타 초기화 작업을 수행합니다.
    }
    
    override func viewDidAppear(_ animated: Bool) {
        super.viewDidAppear(animated)
        // 화면이 나타난 후에 사용자 입력을 처리하거나 다른 작업을 수행합니다.
    }
    
    override func viewWillDisappear(_ animated: Bool) {
        super.viewWillDisappear(animated)
        // 다른 화면으로 이동하기 전에 필요한 작업을 수행합니다.
    }
    
    override func viewDidDisappear(_ animated: Bool) {
        super.viewDidDisappear(animated)
        // 다른 화면으로 이동한 후 필요한 작업을 수행합니다.
    }
}
```

https://github.com/Luna828/luna828.github.io/assets/93186591/9c89fdaa-257b-49e7-85a9-5af2701b6cdb

위의 영상에 보이는 것과 같이 1 - 2 - 3 이 순서대로 실행되어 첫번째의 view를 보여준 후 NavigationController를 타고 첫번째의 view가 4 - 5 로 사라지게 된다
그리고 다시 back 버튼을 사용해 뒤로 가게되면 처음 초기화되는 1. viewDidLoad()는 호출되지 않는다.  


## UINavigationController

* 스토리 보드에서 cmd + shift + L을 하고 NavController 를 선택하여 다른 화면으로 이동 시킬 수 있음
* stack 구조이기 때문에 push, pop 를 사용함
* `initial View Controller` 에 체크를 잘 해줘야함 (안할 경우 view가 안나올 수 있음)

밑의 코드는 viewController.swift 파일에서 UINavigationController를 사용한 예시이다

```swift
class MyContainerViewController: UIViewController {
    override func viewDidLoad() {
        super.viewDidLoad()

        // Add a button to push a new view controller onto the stack
				let button = UIButton(type: .system)
        button.setTitle("Push View Controller", for: .normal)
        button.addTarget(self, action: #selector(pushViewController), for: .touchUpInside)
        button.frame = CGRect(x: 200, y: 200, width: 200, height: 100)
        self.view.addSubview(button)
    }

    @objc func pushViewController() {
        let newViewController = UIViewController()
        newViewController.title = "New View Controller"
				newViewController.view.backgroundColor = .white
        navigationController?.pushViewController(newViewController, animated: true)
    }
}
```

```swift
// UINavigationController 인스턴스 생성
let navigationController = UINavigationController(rootViewController: FirstViewController())

// 루트 뷰 컨트롤러 설정
navigationController.setViewControllers([firstViewController], animated: true)

// 뷰 컨트롤러 Push
navigationController.pushViewController(secondViewController, animated: true)

// 뷰 컨트롤러 Pop
navigationController.popViewController(animated: true)
```

---

메모 메모..
* 생명주기를 잘 숙지하기
* 언제 적절히 쓰이는지 알기 
