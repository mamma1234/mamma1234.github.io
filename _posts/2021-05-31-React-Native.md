---
layout: post
title: "React Native"
description: 
headline: 
modified: 2021-05-31
category: webdevelopment
imagefeature: cover3.jpg
tags: [React Native]
mathjax: 
chart: 
share: true
comments: true
featured: true
disqus:
---

# Record
## 개념
- 
## 시작


```JavaScript
$ npm install -g create-react-native-app

- case 1 : React Native 프로젝트는 CLI보다는 CRNA를 통해서 프로젝트를 시작한 후 ejecting 기능을 사용해 Expo SDK를 그대로 가져가며 프로젝트는 진행하는것이 좋을것 같습니다.
$ create-react-native-app 프로젝트명



- case 2
$ react-native init 프로젝트명


$ cd 프로젝트 명
$ npm start

$ npm install -g react-native-cli

$ cd 프로젝트 명
$ react-native run-ios 
$ react-native run-android

$ react-native run-ios --simulator "iPhone 8"

$ yarn ios

```

## 참조
- [https://wit.nts-corp.com/2020/03/23/6014](https://wit.nts-corp.com/2020/03/23/6014)


## 목차
- [style](#style)
- [RN flex](#rn-flex)
- [component](#component)

## style
- CSS VS RN
  - 각 스타일 속성의 구분은 ;가 아닌 ,로 합니다.
  - 클래스 선택자에  .을 붙이지 않는다.


```JavaScript
* CSS
.bigBlue {
    color: blue;
    font-weight: bold;
    font-size: 30px;
}
.red {
    color: red;
}

* RN
bigBlue: {
    color: 'blue',
    fontWeight: 'bold',
    fontSize: 30,
},
red: { 
    color: 'red',
}
```


- 스타일 속성명(property)의 단어 구분은 하이픈(‘-‘)이 아닌 카멜케이스를 이용

```JavaScript
* CSS
.content {
    justify-content: space-between;
    background-color: #eee;
}

* RN
content: {
    justifyContent: 'space-between',
    backgroundColor: '#eee',
},
```

- 스타일 속성명의 하이픈(‘-’)을 사용
- ‘px’, ‘em’ 등의 단위 사용
- 스타일 우선 순위가 CSS와 다르다.
- 의사 클래스(가상 클래스), 가상요소, 형제 선택자, 자식 선택자 등을 사용할 수 없다
- 스크립트의 장점을 활용할 수 있다.

## RN의 flex
- main axis, CSS의 flex와 RN의 flex는 main axis가 반대

- 지원하지 않는 flex 관련 속성


속성명(property)	|| 값(value)	|| 기본값
flex	|| number	|| 
flexDirection	|| ‘row’ , ‘row-reverse’ , ‘column’ , ‘column-reverse’	|| ‘column’
flexGrow	|| number	|| 0
flexShrink	|| number	|| 1
flexBasis	|| number , string	|| ‘auto’
flexWrap	|| ‘wrap’	|| ‘nowrap’
justifyContent	|| ‘flex-start’ , ‘flex-end’ , ‘center’ , ‘space-between’ , ‘space-around’ , ‘space-evenly’	|| ‘flex-start’
alignItems	|| ‘flex-start’ , ‘flex-end’ , ‘center’ , ‘stretch’ , ‘baseline’	|| ‘stretch’
alignContent	|| ‘flex-start’ , ‘flex-end’ , ‘center’ , ‘stretch’ , ‘space-between’ , ‘space-around’	|| ‘flex-start’
alignSelf	|| ‘auto’ , ‘flex-start’ , ‘flex-end’ , ‘center’ , ‘stretch’ , ‘baseline’	|| ‘stretch’


## component