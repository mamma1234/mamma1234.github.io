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


## 목차
- [Flex Container](#flex-container)
  - [display](#display)
    - [flex-flow](#flex-flow)
      - [flex-direction](#flex-direction)
      - [flex-wrap](#flex-wrap)
    - [justify-content](#justify-content)

## Flex Container

속성 || 의미
display	|| Flex Container를 정의
flex-flow	|| flex-direction와 flex-wrap의 단축 속성
    flex-direction || Flex Items의 주 축(main-axis)을 설정
    flex-wrap	|| Flex Items의 여러 줄 묶음(줄 바꿈) 설정
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





- [https://berkbach.com/service-worker-%EC%97%90-%EA%B4%80%ED%95%B4%EC%84%9C-9c8f9f2f3988](https://berkbach.com/service-worker-%EC%97%90-%EA%B4%80%ED%95%B4%EC%84%9C-9c8f9f2f3988)

- [https://so-so.dev/web/service-worker/](https://so-so.dev/web/service-worker/)


1. 캐시와 상호작용
2. 푸쉬 알림
3. 백그라운드 동기화

