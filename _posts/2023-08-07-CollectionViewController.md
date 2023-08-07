---
title: "[iOS] CollectionView사용시 셀 크기 구현해보기"
layout: single
categories: iOS
tag: [swift, storyboard, TIL, WIL]
toc: true
---

## Collection View의 margin값 설정

![스크린샷 2023-08-07 오후 3 45 44](https://github.com/Luna828/luna828.github.io/assets/93186591/85757f57-af38-4188-8500-4aab6a09da19)


```swift
//모든 마진 값을 10을 주기
let sectionInsets = UIEdgeInsets(top: 10, left: 10, bottom: 10, right: 10)
```

## Collection View Cell Size 설정

셀 사이즈를 동적으로 결정해 줄 때, storyboard에서 설정해주기엔 어려움이 있어 코드로 구현해주는 방법이 훨씬 간편하다

아래의 코드를 해석하자면
1. let width = view.bounds.width는  Collection View 의 가로 크기를 알아오는 코드입니다
2. let itemSpacing: CGFloat = 10 은 셀은 위에 있는 cell들 사이사이의 간격이 10인 것을 뜻합니다
3. let cellWidth = (width - (sectionInset.left + sectionInsets.right) - (itemSpacing * 2)) / 3
  - collection view 가로 크기에서
  - 10 + 10 의 마진 값을 빼주고
  - 예를들어, 내가 가로에 셀을 3개를 두고 싶으면 셀 간격이 2개가 생기기 때문에 그 간격을 또 빼줍니다
  - 마지막으로 나누기 3을 하는 이유는 내가 셀을 3개를 두고 싶기 때문에 그 만큼을 나눠주는 것입니다
4. retrun CGSize(width: height:) 값을 설정해주면 끝!!

<img src="https://github.com/Luna828/luna828.github.io/assets/93186591/a2933b6b-0330-4f04-98e1-b9e9da176a2e" width="250" height="500"/>

```swift

extension showMemoCollectionViewController: UICollectionViewDelegateFlowLayout {
    
    //셀 사이즈를 결정해주는 코드
    func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, sizeForItemAt indexPath: IndexPath) -> CGSize {
        let width = view.bounds.width
        let itemSpacing: CGFloat = 10 //셀 사이 간격 너비
        let cellWidth: CGFloat = (width - (sectionInsets.left + sectionInsets.right) - (itemSpacing * 2)) / 3
        return CGSize(width: cellWidth, height: cellWidth)
    }
}

```

다른 예시로 

```swift
let cellWidth = (width - (sectionInset.left + sectionInsets.right) - (itemSpacing * 3)) / 4
```
<img src="https://github.com/Luna828/luna828.github.io/assets/93186591/76dd7d1d-aa90-41ce-8815-64e3d76726c3" width="250" height="500"/>

위의 사진과 같이 셀의 크기는 동적으로 작아지면서 가로에 셀이 4개가 배치되는 것을 볼 수 있다!
공식같은 느낌 ㅎ


## CollectionViewController 전체 구현 코드

```swift
import UIKit

class showMemoCollectionViewController: UIViewController, UICollectionViewDelegate, UICollectionViewDataSource {
    let sectionInsets = UIEdgeInsets(top: 10, left: 10, bottom: 10, right: 10)
    
    @IBOutlet weak var myCollectionView: UICollectionView!
    
    override func viewDidLoad() {
        super.viewDidLoad()

        //collectionview 설정
        //myCollectionView.autoresizingMask = [.flexibleWidth, .flexibleHeight]
        myCollectionView.dataSource = self
        myCollectionView.delegate = self
        //myCollectionView.contentInset = sectionInsets
    }
    
    override func viewWillAppear(_ animated: Bool) {
        super.viewWillAppear(animated)
        
        //table view 목록 업데이트
        DataManager.shared.fetchMemo()
    }
    
 //sectionInsets의 공간 만큼 추가되기 때문에 cell이 벌려짐 (전체 패딩) = viewDidLoad()의 myCollectionView.contentInset = sectionInsets 랑 같음
    func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, insetForSectionAt section: Int) -> UIEdgeInsets {

        return sectionInsets
    }
    
    // 각 콜렉션뷰 쎌 설정
    func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell {
        
        let cell = collectionView.dequeueReusableCell(withReuseIdentifier: "CollectionViewCell", for: indexPath) as! memoClass
        cell.collectionBtn.setTitle(DataManager.shared.memoList[indexPath.row].content, for: .normal)
        
        return cell
    }
    
    func collectionView(_ collectionView: UICollectionView, numberOfItemsInSection section: Int) -> Int {
        print(DataManager.shared.memoList.count)
        return DataManager.shared.memoList.count
    }
}


extension showMemoCollectionViewController: UICollectionViewDelegateFlowLayout {
    
    //셀 사이즈를 결정해주는 코드
    func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, sizeForItemAt indexPath: IndexPath) -> CGSize {
        let width = view.bounds.width
        let itemSpacing: CGFloat = 10 //셀 사이 간격 너비
        let cellWidth: CGFloat = (width - (sectionInsets.left + sectionInsets.right) - (itemSpacing * 2)) / 3
        return CGSize(width: cellWidth, height: cellWidth)
    }
}

class memoClass: UICollectionViewCell {
    @IBOutlet weak var collectionBtn: UIButton!
}

```

collection view 에 대해 처음 도전해보는 날이었는데!!많은 걸 알아가는 시간이었다!!!

코드로 cell size 를 구현할 수 있게 해준 지욱님, 준우님, 준영님 감사드립니다 ~~ 


