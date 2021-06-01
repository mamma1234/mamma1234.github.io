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
    - [View](#view)
    - [Text](#text)
    - [Touchable](#touchable)
    - [Image](#image)


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

### View
- View 컴포넌트는 UI를 구축하기 위한 가장 기본적인 구성요소로서 웹에서는 div와 사용성이 유사합니다. 중첩이 가능하며 레이아웃을 구축하기 위해서 가장 많이 사용합니다. 일부 터치 핸들링 및 접근성 제어가 가능합니다.

### Text
- Text는 텍스트를 표현하기 위한 컴포넌트로 리액트 네이티브에서 기본적으로 제공하는 컴포넌트에서는 Text와 TextInput을 사용해야만 텍스트를 삽입할 수 있기 때문에 필수적으로 사용되는 컴포넌트입니다.
Text 내부에 사용할 수 있는 컴포넌트는 매우 제한적이며 내부 요소의 스타일 제약을 받을 수 있습니다.


### Touchable
- button 역할을 하는 컴포넌트

#### Button
- 기본적인 버튼 컴포넌트입니다. style props를 이용해 스타일링을 할 수 없기 때문에 UI개발시 활용도가 떨어집니다.
    - color : ios의 경우 버튼 텍스트 color, 안드로이드의 경우 버튼 배경색이 변경됩니다.

#### TouchableHightlight
- 터치시 하이라이트가 발생합니다. 내부에 반드시 하나의 자식 컴포넌트를 삽입해야합니다.
여러개의 컴포넌트가 필요하다면 View나 flagment(<></>)를 이용해 그룹화해야합니다.
    - underlayColor : 터치시 하이라이팅되는 색상을 지정합니다.

#### TouchableOpacity
- 터치시 opacity값이 적용됩니다. 다른 Touchable 컴포넌트와 달리 여러개의 자식 요소가 올 수 있습니다.
    - activeOpacity : 터치시 적용되는 opacity값을 설정합니다.(0~1)

#### TouchableNativeFeedback
- 터치시 사용자가 정의한 피드백을 표현할 수 있으며 단일 View 컴포넌트만 자식 요소로 가질 수 있습니다. Android 환경만 지원합니다.

### Image