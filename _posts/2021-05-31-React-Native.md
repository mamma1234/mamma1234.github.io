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
    - [ImageBackground](#imagebackground)
    - [SafeAreaView](#safeareaView)
    - [ScrollView](#scrollview)
    - [KeyboardAvodingView](#keyboardavodingview)
    - [FlatList](#flatlist)
    - [ActiveIndicator](#activeindicator)
    - [Modal](#modal)
- [커스텀 컴포넌트 사용하기](#커스텀-컴포넌트-사용하기)


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

## RN flex
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
- html의 img태그처럼 이미지를 표현할 때 사용하는 컴포넌트입니다. source props에 이미지 경로를 전달해 사용합니다.
앱 내부의 이미지파일을 불러올 땐 require를 이용하며 width, height를 적용하지 않으면 이미지 원본의 사이즈대로 렌더링됩니다.
네트워크 이미지나 데이터 url 이미지를 사용할 때는 image의 width, height 등 영역을 확보해주지 않으면 영역이 잡히지 않습니다.

### ImageBackground
- background 관련 스타일은 backgroundColor만 존재하는 리액트 네이티브에서 배경이미지를 필요할 때 사용하는 컴포넌트 입니다.

### SafeAreaView
- SafeAreaView는 기기의 안전한 영역 경계 내에서 콘텐츠를 렌더링할 때 사용합니다.
만약 SafeAreaView를 적용하지 않는다면 기기의 둥근 코너나 카메라 노치와 같은 화면의 물리적인 부분과, 탐색 모음, 탭 바, 시간, 배터리 등 도구 모음 등의 뷰가 렌더링되는 내용과 겹치는 현상이 발생하게됩니다.
SafeAreaView는 자동으로 padding을 적용하여 위와 같은 문제를 해결하고 안전한 영역에 콘텐츠가 렌더링될 수 있도록 합니다.
현재 ios 11 버전 이상의 ios기기에만 적용되며 보통 페이지의 최상위 래퍼 컴포넌트로 많이 사용합니다.

### ScrollView
- RN은 웹 브라우저처럼 컨텐츠가 길어지면 자동적으로 스크롤을 생성하지 않습니다.
스크롤이 필요하다면 ScrollView 컴포넌트를 사용하며 CSS에서 요소에 overflow: auto을 선언한 것과 유사하게 동작합니다.
RN은 position: 'fixed'를 지원하지 않지만 ScrollView를 사용해야만 스크롤이 생성되기 때문에 뷰포트에 고정된 UI를 구현할 수 있습니다.
또한 horizontal props를 통해 가로 스크롤을 제어할 수 있습니다.
ScrollView는 flex: 1이 기본 값으로 설정되어있습니다.

### KeyboardAvodingView
- KeyboardAvodingView는 키보드가 올라올 경우 컨텐츠가 키보드에 가려지는 문제를 해결하는 방법을 제공하는 컴포넌트입니다.
behavior props를 이용해 키보드 회피 방법을 정할 수 있습니다.
input이 제공되어 키보드를 사용해야하는 페이지에서 필수적으로 사용되는 컴포넌트입니다.



### FlatList
- FlatList는 목록형 UI를 렌더링 할 때 유용한 기능을 제공하는 컴포넌트입니다. 목록이 길어지면 자동적으로 내부에 ScrollView가 적용되므로 데이터에 따라 스크롤 처리가 필요하다면 ScrollView보다 좋은 선택일 수 있습니다. header, footer, 데이터가 없을 경우 노출될 UI, 아래로 당겼을 때 refresh 기능 등을 props를 통해 설정할 수 있으며 행 별로 스타일 제어가 가능해 그리드 UI를 구현할 때도 매우 편리합니다. data와 renderItem props는 필수적으로 선언해주어야합니다

### ActiveIndicator
- 로딩시 로딩 인디케이터를 제공하는 컴포넌트입니다. OS마다 인디케이터 모양이 다르고 사이즈는 large, small로만 제어할 수 있어 로딩 인디케이터 디자인이 따로 적용되어 있거나 정확한 사이즈를 조정해야한다면 사용하기 힘든 단점이 있습니다.


### Modal
- 모달창을 구현할 때 사용되는 컴포넌트입니다. 어디에 선언되든 부모와 상관없이 항상 뷰포트 전체 width, height값을 가지며 기존 레이아웃 위에 노출됩니다.


## 커스텀 컴포넌트 사용하기
- RN에서 제공하는 컴포넌트를 사용하면서 컴포넌트 내에 항상 들어가는 코드가 있다면 커스텀 컴포넌트를 사용을 고려해 볼 수 있습니다.
반복적인 코드나 스타일 리셋 코드 등을 넣어 컴포넌트를 사용한다면 코드를 매번 삽입할 필요가 없어집니다.
저희 서비스에서는 안드로이드 환경에서 폰트에 들어가는 padding값을 없애기 위해서 RN에서 제공하는 Text를 커스텀해 사용하였습니다.

```JavaScript
import * as React from 'react'
import { Text, Platform, TextProps } from 'react-native'

const DefaultStyle = Platform.select({
  ios: {},
  android: { includeFontPadding: false },
})

const wrappedText: React.SFC<TextProps> = ({ children, style, ...bypass }) => (
  <Text {...bypass} style={[DefaultStyle, style]}>
    {children}
  </Text>
)

export default wrappedText
```