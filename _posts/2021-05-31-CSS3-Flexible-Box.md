---
layout: post
title: "CSS3 Flexible Box"
description: 
headline: 
modified: 2021-05-31
category: webdevelopment
imagefeature: cover3.jpg
tags: [CSS3 Flexible Box]
mathjax: 
chart: 
share: true
comments: true
featured: true
disqus:
---

# Record
## 개념
- Flex는 요소의 크기가 불분명하거나 동적인 경우에도, 각 요소를 정렬할 수 있는 효율적인 방법을 제공  

- Container, Items 구분
  - Container에는 display, flex-flow, justify-content 등의 속성을 사용할 수 있으며,
  - Items에는 order, flex, align-self 등의 속성을 사용할 수 있습니다.

## 참조
- [https://flexboxfroggy.com/#ko](https://flexboxfroggy.com/#ko)
- [https://heropy.blog/2018/11/24/css-flexible-box/](https://heropy.blog/2018/11/24/css-flexible-box/)
- [https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox](https://developer.mozilla.org/ko/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox)

## 목차
- [Flex Container](#flex-container)
  - [display](#display)
  - [flex-flow](#flex-flow)
    - [(중요) flex-direction](#flex-direction)
    - [flex-wrap](#flex-wrap)
  - [(중요) justify-content](#justify-content)
  - [align-content](#align-content)	
  - [(중요) align-items](#align-items)
- [Flex Items](#flex-items)
  - [(중요) order](#order)
  - [flex](#flex)
    - [flex-grow](#flex-grow)
    - [flex-shrink](#flex-shrink)
    - [flex-basis](#flex-basis)
  - [(중요) align-self](#align-self)

order	|| Flex Item의 순서를 설정
flex	|| flex-grow, flex-shrink, flex-basis의 단축 속성
  >> flex-grow	|| Flex Item의 증가 너비 비율을 설정
  >> flex-shrink	|| Flex Item의 감소 너비 비율을 설정
  >> flex-basis	|| Flex Item의 (공간 배분 전) 기본 너비 설정
align-self	|| 교차 축(cross-axis)에서 Item의 정렬 방법을 설정



## Flex Container

속성 || 의미
display	|| Flex Container를 정의
flex-flow	|| flex-direction와 flex-wrap의 단축 속성
  >> flex-direction || Flex Items의 주 축(main-axis)을 설정
  >> flex-wrap	|| Flex Items의 여러 줄 묶음(줄 바꿈) 설정
justify-content	|| 주 축(main-axis)의 정렬 방법을 설정
align-content	|| 교차 축(cross-axis)의 정렬 방법을 설정(2줄 이상)
align-items	|| 교차 축(cross-axis)에서 Items의 정렬 방법을 설정(1줄)


### display

값 || 의미 ||	기본값 || 설명
flex || Block 특성의 Flex Container를 정의	|| || 지정된 Flex Container는 Block 요소와 같은 성향(수직 쌓임)
inline-flex || Inline 특성의 Flex Container를 정의 ||  || 지정된 Flex Container는 Inline(Inline Block) 요소와 같은 성향(수평 쌓임)


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


## Flex Items

속성	|| 의미
order	|| Flex Item의 순서를 설정
flex	|| flex-grow, flex-shrink, flex-basis의 단축 속성
  >> flex-grow	|| Flex Item의 증가 너비 비율을 설정
  >> flex-shrink	|| Flex Item의 감소 너비 비율을 설정
  >> flex-basis	|| Flex Item의 (공간 배분 전) 기본 너비 설정
align-self	|| 교차 축(cross-axis)에서 Item의 정렬 방법을 설정


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

