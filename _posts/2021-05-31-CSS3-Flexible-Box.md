---
layout: post
title: "CSS3 Flexible Box"
description: 
headline: 
modified: 2021-04-30
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
- [https://heropy.blog/2018/11/24/css-flexible-box/](https://heropy.blog/2018/11/24/css-flexible-box/)


## 목차
- [Flex Container](#flex-container)
  - [display](#display)
    - [flex-flow](#flex-flow)
      - [flex-direction](#flex-direction)
      - [flex-wrap](#flex-wrap)
    - [justify-content](#justify-content)
    - [align-content](#align-content)	
    - [align-items](#align-items)
- [Flex Items](#flex-items)

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


1. 캐시와 상호작용
2. 푸쉬 알림
3. 백그라운드 동기화

