---
layout: post
title: "CSS3 Grid"
description: 
headline: 
modified: 2021-05-31
category: webdevelopment
imagefeature: cover3.jpg
tags: [CSS3 Grid]
mathjax: 
chart: 
share: true
comments: true
featured: true
disqus:
---

# Record
## 개념
- CSS Grid(그리드)는 2차원(행과 열)의 레이아웃 시스템을 제공합니다.
Flexible Box도 훌륭하지만 비교적 단순한 1차원 레이아웃을 위하며, 좀 더 복잡한 레이아웃을 위해 우리는 CSS Grid를 사용할 수 있습니다.  

- CSS Grid는 CSS Flex와 같이 Container(컨테이너)와 Item(아이템)이라는 두 가지 개념으로 구분되어 있습니다.
Container는 Items를 감싸는 부모 요소이며, 그 안에서 각 Item을 배치할 수 있습니다.

## 참조
- [https://cssgridgarden.com/#ko](https://cssgridgarden.com/#ko)
- [https://heropy.blog/2019/08/17/css-grid/](https://heropy.blog/2019/08/17/css-grid/)
- [https://developer.mozilla.org/ko/docs/Web/CSS/grid](https://developer.mozilla.org/ko/docs/Web/CSS/grid)

## 목차
- [Grid Container](#grid-Container)
  - [display](#display)
  - [flex-flow](#flex-flow)
    - [flex-direction](#flex-direction)
    - [flex-wrap](#flex-wrap)
  - [justify-content](#justify-content)
  - [align-content](#align-content)	
  - [align-items](#align-items)
- [Grid Items](#grid-items)
  - [order](#order)
  - [flex](#flex)
    - [flex-grow](#flex-grow)
    - [flex-shrink](#flex-shrink)
    - [flex-basis](#flex-basis)
  - [align-self](#align-self)


## Grid Container

속성 || 의미
display	|| 그리드 컨테이너(Container)를 정의
grid-template-rows	|| 명시적 행(Track)의 크기를 정의
grid-template-columns	|| 명시적 열(Track)의 크기를 정의
grid-template-areas	|| 영역(Area) 이름을 참조해 템플릿 생성
grid-template	|| grid-template-xxx의 단축 속성
row-gap(grid-row-gap)	|| 행과 행 사이의 간격(Line)을 정의
column-gap(grid-column-gap)	|| 열과 열 사이의 간격(Line)을 정의
gap(grid-gap)	|| xxx-gap의 단축 속성
grid-auto-rows	|| 암시적인 행(Track)의 크기를 정의
grid-auto-columns	|| 암시적인 열(Track)의 크기를 정의
grid-auto-flow	|| 자동 배치 알고리즘 방식을 정의
grid	|| grid-template-xxx과 grid-auto-xxx의 단축 속성
align-content	|| 그리드 콘텐츠(Grid Contents)를 수직(열 축) 정렬
justify-content	|| 그리드 콘텐츠를 수평(행 축) 정렬
place-content	|| align-content와 justify-content의 단축 속성
align-items	|| 그리드 아이템(Items)들을 수직(열 축) 정렬
justify-items	|| 그리드 아이템들을 수평(행 축) 정렬
place-items	|| align-items와 justify-items의 단축 속성


### display

값	|| 의미
grid	|| Block 특성의 Grid Container를 정의
inline-grid	|| Inline 특성의 Grid Container를 정의

### flex-flow

값	|| 의미	|| 기본값
flex-direction	|| Items의 주 축(main-axis)을 설정	|| row
flex-wrap	|| Items의 여러 줄 묶음(줄 바꿈) 설정	|| nowrap

#### flex-direction

- Items의 주 축(main-axis)을 설정합니다.

값	|| 의미	|| 기본값
row	|| Itmes를 수평축(왼쪽에서 오른쪽으로)으로 표시	|| row
row-reverse	|| Items를 row의 반대 축으로 표시	||
column	|| Items를 수직축(위에서 아래로)으로 표시	||
column-reverse	|| Items를 column의 반대 축으로 표시 ||


- 주 축(main-axis)과 교차 축(cross-axis) : 방향(수평, 수직)에 따라 주 축과 교차 축이 달라집니다.
- 시작점(flex-start)과 끝점(flex-end) : 방향에 따라 시작점과 끝점이 달라집니다

#### flex-wrap

- Items의 여러 줄 묶음(줄 바꿈)을 설정합니다.

값	|| 의미	|| 기본값
nowrap	|| 모든 Itmes를 여러 줄로 묶지 않음(한 줄에 표시)	|| nowrap
wrap	||Items를 여러 줄로 묶음	||
wrap-reverse	|| Items를 wrap의 역 방향으로 여러 줄로 묶음 ||


### justify-content

- 주 축(main-axis)의 정렬 방법을 설정합니다.

값	|| 의미	|| 기본값
flex-start	|| Items를 시작점(flex-start)으로 정렬	|| flex-start
flex-end	|| Items를 끝점(flex-end)으로 정렬 ||	
center	|| Items를 가운데 정렬	||
space-between	|| 시작 Item은 시작점에, 마지막 Item은 끝점에 정렬되고 나머지 Items는 사이에 고르게 정렬됨	 ||
space-around	|| Items를 균등한 여백을 포함하여 정렬 ||


### align-content	

- 교차 축(cross-axis)의 정렬 방법을 설정합니다.
* 주의할 점은 flex-wrap 속성을 통해 Items가 여러 줄(2줄 이상)이고 여백이 있을 경우만 사용할 수 있습니다.
* Items가 한 줄일 경우 align-items 속성을 사용하세요.

값	|| 의미	|| 기본값
stretch	|| Container의 교차 축을 채우기 위해 Items를 늘림	|| stretch
flex-start	|| Items를 시작점(flex-start)으로 정렬 ||	
flex-end	|| Items를 끝점(flex-end)으로 정렬	||
center	|| Items를 가운데 정렬	||
space-between	|| 시작 Item은 시작점에, 마지막 Item은 끝점에 정렬되고 나머지 Items는 사이에 고르게 정렬됨	||
space-around	|| Items를 균등한 여백을 포함하여 정렬 ||

### align-items

- 교차 축(cross-axis)에서 Items의 정렬 방법을 설정합니다.
  * Items가 한 줄일 경우 많이 사용합니다.
  * 주의할 점은 Items가 flex-wrap을 통해 여러 줄(2줄 이상)일 경우에는 align-content 속성이 우선합니다. 따라서 align-items를 사용하려면 align-content 속성을 기본값(stretch)으로 설정해야 합니다.

값	|| 의미	|| 기본값
stretch	|| Container의 교차 축을 채우기 위해 Items를 늘림	|| stretch
flex-start	|| Items를 각 줄의 시작점(flex-start)으로 정렬	||
flex-end	|| Items를 각 줄의 끝점(flex-end)으로 정렬	||
center	|| Items를 가운데 정렬	||
baseline	|| Items를 문자 기준선에 정렬 ||


## Grid Items

속성	|| 의미
grid-row-start	|| 그리드 아이템(Item)의 행 시작 위치 지정
grid-row-end	|| 그리드 아이템의 행 끝 위치 지정
grid-row	|| grid-row-xxx의 단축 속성(행 시작/끝 위치)
grid-column-start	|| 그리드 아이템의 열 시작 위치 지정
grid-column-end	|| 그리드 아이템의 열 끝 위치 지정
grid-column	|| grid-column-xxx의 단축 속성(열 시작/끝 위치)
grid-area	|| 영역(Area) 이름을 설정하거나, grid-row와 grid-column의 단축 속성
align-self	|| 단일 그리드 아이템을 수직(열 축) 정렬
justify-self	|| 단일 그리드 아이템을 수평(행 축) 정렬
place-self	|| align-self와 justify-self의 단축 속성
order	|| 그리드 아이템의 배치 순서를 지정
z-index	|| 그리드 아이템의 쌓이는 순서를 지정


### order

- Item의 순서를 설정합니다.
  * Item에 숫자를 지정하고 숫자가 클수록 순서가 밀립니다.
  * 음수가 허용됩니다.

값	|| 의미	|| 기본값
숫자	|| Item의 순서를 설정	|| 0


### flex
- Item의 너비(증가, 감소, 기본)를 설정하는 단축 속성입니다.

값	|| 의미	|| 기본값
flex-grow	|| Item의 증가 너비 비율을 설정	|| 0
flex-shrink	|| Item의 감소 너비 비율을 설정	|| 1
flex-basis	|| Item의 (공간 배분 전) 기본 너비 설정	|| auto


```JavaScript
.item {
  flex: 1 1 20px;  /* 증가너비 감소너비 기본너비 */
  flex: 1 1;  /* 증가너비 감소너비 */
  flex: 1 20px;  /* 증가너비 기본너비 (단위를 사용하면 flex-basis가 적용됩니다) */
}
```


#### flex-grow
- Item의 증가 너비 비율을 설정합니다.
  * 숫자가 크면 더 많은 너비를 가집니다.
  * Item이 가변 너비가 아니거나, 값이 0일 경우 효과가 없습니다.

값	|| 의미	|| 기본값
숫자	|| Item의 증가 너비 비율을 설정	|| 0

  * 모든 Items의 총 증가 너비(flex-grow)에서 각 Item의 증가 너비의 비율 만큼 너비를 가질 수 있습니다.
  예를 들어 Item이 3개이고 증가 너비가 각각 1, 2, 1이라면,
  첫 번째 Item은 총 너비의 25%(1/4)을,
  두 번째 Item은 총 너비의 50%(2/4)를,
  세 번째 Item은 총 너비의 25%(1/4)을 가지게 됩니다.


#### flex-shrink
- Item이 감소하는 너비의 비율을 설정합니다.
숫자가 크면 더 많은 너비가 감소합니다.
Item이 가변 너비가 아니거나, 값이 0일 경우 효과가 없습니다.

값	|| 의미	|| 기본값
숫자	|| Item의 감소 너비 비율을 설정	|| 1


#### flex-basis
- Item의 (공간 배분 전) 기본 너비를 설정합니다.
값이 auto일 경우 width, height 등의 속성으로 Item의 너비를 설정할 수 있습니다.
하지만 단위 값이 주어질 경우 설정할 수 없습니다.

값	|| 의미	|| 기본값
auto	|| 가변 Item과 같은 너비	|| auto
단위	|| px, em, cm 등 단위로 지정	||

  * flex 속성에서 설명한 것 같이 단축 속성 내에서 flex-basis를 생략하면 값이 0이 되는 것을 주의합시다

### align-self
- 교차 축(cross-axis)에서 개별 Item의 정렬 방법을 설정합니다.

  * align-items는 Container 내 모든 Items의 정렬 방법을 설정합니다.
  필요에 의해 일부 Item만 정렬 방법을 변경하려고 할 경우 align-self를 사용할 수 있습니다.
  이 속성은 align-items 속성보다 우선합니다.

값	|| 의미	|| 기본값
auto	|| Container의 align-items 속성을 상속받음	|| auto
stretch	|| Container의 교차 축을 채우기 위해 Item을 늘림	||
flex-start	|| Item을 각 줄의 시작점(flex-start)으로 정렬	||
flex-end	|| Item을 각 줄의 끝점(flex-end)으로 정렬	||
center	|| Item을 가운데 정렬	||
baseline	|| Item을 문자 기준선에 정렬 ||

