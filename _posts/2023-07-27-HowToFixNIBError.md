---
title: "[swift] Thread 1: unable to dequeue a cell with identifier tableViewCell - must register a nib or a class for the identifier or connect a prototype cell in a storyboard 에러 해결"
layout: single
categories: Error
tag: [swift, error, TIL, WIL]
toc: true
---


## Xib 파일을 연결하면서 생긴 에러

캠프에서 나 외 몇명과 함께 따로 스토리 보드 예습을 하기 위해서 저녁 9시부터 12시까지 뭉치게되면서.. 아이폰 설정을 보면서 각자 만들어오기로 약속했다!
그.런.데..
4명중 3명이 지금 이 밑에 써져있는 에러메세지를 만나면서 삽질하는 시간을 보내게 되었다.. 몇시간동안 헤맸는지 상상도 안간다 (^^)

AppDelegate.swift 파일에서

1. Thread 1: "unable to dequeue a cell with identifier TableViewNameCell - must register a nib or a class for the identifier or connect a prototype cell in a storyboard"

2. Thread 1: "Could not load NIB in bundle: 'NSBundle </Users/내컴퓨터이름/Library/Developer/CoreSimulator/Devices/DBECFF67-2531-411F-978C-3F39E35D155F/data/Containers/Bundle/Application/85746C9E-7C5C-4EC4-B7F3-822F915564C9/SampleUIKit.app> (loaded)' with name 'TableViewNameCell'"


## 에러 해결 방안

강의를 따라해보면서 혹시나 잘못 따라한건 아닌지 몇번을 보다가 "교수님"이라고 불리는 한 사람의 도움을 받아서!! 
정말 어이없게 찾아버렸다 ㅠㅠ (난 왜..또.. 왜.. 내가 찾질 못하는거야!!!)

1. 일단 xib 파일에 인스펙터 부분에 Identifier를 설정해 주지않은 것!! 
-> 이것을 설정하면 unable to dequeue a cell with identifier TableViewNameCell 이 Error는 없어진다
![KakaoTalk_Photo_2023-07-27-15-06-50 002](https://github.com/Luna828/luna828.github.io/assets/93186591/c83f1447-d0bf-4932-87e0-50d79c58dcdf)
![KakaoTalk_Photo_2023-07-27-15-06-50 003](https://github.com/Luna828/luna828.github.io/assets/93186591/cfa8f937-3653-4f51-b738-ab6e61fab692)
2. 그 다음으로는 main storyboard tableView에 table view cell을 넣어주지 않은 것 
-> 이것을 해주지않으면 simulator를 돌렸을 때 화면에 cell들이 그려지지 않는다
![스크린샷 2023-07-27 오후 3 10 39](https://github.com/Luna828/luna828.github.io/assets/93186591/d24dfbe8-32e8-4acb-b17b-d5e3079a48fc)
3. 진짜 가장 어이없었던... TableViewNameCell.xib 파일과 xib파일을 연결시켜둔 TableViewNameCell.swift 파일 이름이 똑같이 않아서이다...
-> 처음에 강의를 따라하면서 정신없이 따라하다보니 TableViewNameCell.xib라고 만들어두고 swift파일은 TableViewCell이라고 설정해둔 것이다... 그래서 xcode가 실행되면서 nibName에 연결된 것을 찾을 수 없다고 위의 Could not load NIB in bundle: 'NSBundle  이 에러가 뜬 것이었다.. 

![KakaoTalk_Photo_2023-07-27-15-06-50 001](https://github.com/Luna828/luna828.github.io/assets/93186591/be3c619d-7d42-4e5c-a0f1-04649ea43573)


이 세개를 잘 설정하면 Nib Error는 잘 해결할 수 있지 않을까한다... ㅠㅠ 
