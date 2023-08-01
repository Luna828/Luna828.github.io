---
title: "[iOS] NSUnknownKeyException Error"
layout: single
categories: Error
tag: [swift, storyboard, error, TIL, WIL]
toc: true
---

## 에러 발생

Memo App을 만들던 도중 MemoCell.xib 파일을 만들어 Table Cell을 새로 구성하고 

* identifier

* MemoCell.swift 파일 연결

* @IBOutlet weak var memoTitle: UILabel! 연결

* MemoTableViewController class 연결

이 모든 것을 다 연결했음에도 불구하고 밑에 어마무시한 Error 영어가 나타남...

```
'NSUnknownKeyException', reason: '[<UITableViewCell 0x129d101f0> setValue:forUndefinedKey:]: this class is not key value coding-compliant for the key memoDate.'
```

## 에러 해결

내배캠 튜터님과 같이 구글링해서 찾은 결과..!
Custom Class의 Module - Inherit Module From Target에 체크가 되어있지 않아 생긴 문제였다!!!

![스크린샷 2023-08-01 오후 8 35 03](https://github.com/Luna828/luna828.github.io/assets/93186591/ff3c15fb-b529-4d07-aa28-24cdeced5d0e)



