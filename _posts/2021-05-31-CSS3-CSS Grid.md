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
  - [grid-template-rows](#grid-template-rows)
  - [grid-template-columns](#grid-template-columns)
  - [grid-template-areas](#grid-template-areas)
  - [grid-template](#grid-template)
  - [row-gap(grid-row-gap)](#row-gap)
  - [column-gap(grid-column-gap)](#column-gap)
  - [gap(grid-gap)](#gap)
  - [grid-auto-rows](#grid-auto-rows)
  - [grid-auto-columns](#grid-auto-columns)
  - [grid-auto-flow](#grid-auto-flow)
  - [grid](#grid)
  - [align-content](#align-content)
  - [justify-content](#justify-content)
  - [place-content](#place-content)
  - [align-items](#align-items)
  - [justify-items](#justify-items)
  - [place-items](#place-items)
- [Grid Items](#grid-Items)
  - [grid-row-start](#grid-row-start)
  - [grid-row-end](#grid-row-end)
  - [grid-row](#grid-row)
  - [grid-column-start](#grid-column-start)
  - [grid-column-end](#grid-column-end)
  - [grid-column](#grid-column)
  - [grid-area](#grid-area)
  - [align-self](#align-self)
  - [justify-self](#justify-self)
  - [place-self](#place-self)
  - [order](#order)
  - [z-index](#z-index)
- [Grid Functions](#grid-functions)
  - [repeat](#repeat)
  - [minmax](#minmax)
  - [fit-content](#fit-content)
- [Grid Units](#grid-units)
  - [fr](#fr)
  - [min-content](#min-content)
  - [max-content](#max-content)
  - [auto-fill, auto-fit](#auto-fill,-auto-fit)
- [용어 정리](#용어-정리)
  - [Track](#Track)
  - [Line](#Line)
  - [Cell](#Cell)
  - [Area](#Area)



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

### grid-template-rows

- 명시적 행(Track)의 크기를 정의합니다.
- 동시에 라인(Line)의 이름도 정의할 수 있습니다.
- fr(fraction, 공간 비율) 단위를 사용할 수 있습니다.    
      grid-template-columns: repeat(12, 1fr);
- repeat() 함수를 사용할 수 있습니다.                 
      grid-template-columns: repeat(12, 100px);

### grid-template-columns

- 명시적 열(Track)의 크기를 정의합니다.
- 동시에 라인(Line)의 이름도 정의할 수 있습니다.
- fr(fraction, 공간 비율) 단위를 사용할 수 있습니다.
- repeat() 함수를 사용할 수 있습니다.


### grid-template-areas

- 지정된 그리드 영역 이름(grid-area)을 참조해 그리드 템플릿을 생성합니다.
- (마침표)를 사용하거나 명시적으로 none을 입력해 빈 영역을 정의할 수 있습니다.

```JavaScript

.container {
  display: grid;
  grid-template-rows: repeat(4, 100px);
  grid-template-columns: repeat(3, 1fr);
  grid-template-areas:
    "header header header"
    "main . ."
    "main . aside"
    "footer footer footer";
}
header { grid-area: header; }
main   { grid-area: main;   }
aside  { grid-area: aside;  }
footer { grid-area: footer; }

```

### grid-template

- grid-template-rows, grid-template-columns 그리고 grid-template-areas의 단축 속성입니다.

```JavaScript

.container {
  display: grid;
  grid-template:
    "header header header" 80px
    "main main aside" 350px
    "footer footer footer" 130px
    / 2fr 100px 1fr;
}
header { grid-area: header; }
main   { grid-area: main; }
aside  { grid-area: aside; }
footer { grid-area: footer; }


.container {
  display: grid;
  grid-template-rows: 80px 350px 130px;
  grid-template-columns: 2fr 100px 1fr;
  grid-template-areas:
    "header header header"
    "main main aside"
    "footer footer footer";
}

```

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


### row-gap(grid-row-gap)

- 각 행과 행 사이의 간격(Gutter)을 지정합니다.

### column-gap (grid-column-gap)

- 각 열과 열 사이의 간격(Gutter)을 지정합니다.

### gap (grid-gap)

- 각 행과 행, 열과 열 사이의 간격(Gutter)을 지정합니다.

```JavaScript

.container {
  gap: <grid-row-gap> <grid-column-gap>;
}

```

### grid-auto-rows

- 암시적 행(Track)의 크기를 정의합니다.
아이템(Item)이 grid-template-rows로 정의한 명시적 행 외부에 배치되는 경우 암시적 행의 크기가 적용됩니다.

```JavaScript

.container {
  width: 300px;
  height: 200px;
  display: grid;
  grid-template-rows: 100px 100px; /* 명시적 2개 행 정의 */
  grid-template-columns: 150px 150px; /* 명시적 2개 열 정의 */
  grid-auto-rows: 100px; /* 그 외(암시적) 행의 크기 정의 */
}
.item:nth-child(3) {
  grid-row: 3 / 4;
}

```

### grid-auto-columns

- 암시적 열(Track)의 크기를 정의합니다.
아이템(Item)이 grid-template-columns로 정의한 명시적 열 외부에 배치되는 경우 암시적 열의 크기가 적용됩니다.


```JavaScript

.container {
  width: 300px;
  height: 200px;
  display: grid;
  grid-template-rows: 100px 100px;
  grid-template-columns: 150px 150px;
  grid-auto-rows: 100px;
  grid-auto-columns: 100px;
}
.item:nth-child(3) {
  grid-row: 3 / 4;
  grid-column: 3 / 4;
}


```

### grid-auto-flow

- 배치하지 않은 아이템(Item)을 어떤 방식의 ‘자동 배치 알고리즘’으로 처리할지 정의합니다.

값	|| 의미	|| 기본값
row	|| 각 행 축을 따라 차례로 배치	|| row
column	|| 각 열 축을 따라 차례로 배치	
row dense(dense)	|| 각 행 축을 따라 차례로 배치, 빈 영역 메움!	
column dense	|| 각 열 축을 따라 차례로 배치, 빈 영역 메움!	

```JavaScript

/* For row & row dense */
.container {
  display: grid;
  grid-template-rows: repeat(3, 1fr);
  grid-template-columns: repeat(3, 1fr);
  grid-auto-flow: row || row dense || dense;
}
.item:nth-child(2) {
  grid-column: span 3;
}

```

### grid

- grid-template-xxx과 grid-auto-xxx의 단축 속성입니다.

```JavaScript

.container {
  grid: <grid-template>;
  grid: <grid-template-rows> / <grid-auto-flow> <grid-auto-columns>;
  grid: <grid-auto-flow> <grid-auto-rows> / <grid-template-columns>;
}


.container {
  grid: <grid-template>;
}
.container {
  grid:
    "header header header" 80px
    "main main aside" 350px
    "footer footer footer" 130px
    / 2fr 100px 1fr;
}
.container {
  grid-template:
    "header header header" 80px
    "main main aside" 350px
    "footer footer footer" 130px
    / 2fr 100px 1fr;
}

```

### align-content

- 그리드 콘텐츠(Contents)를 수직(열 축) 정렬합니다.
그리드 콘텐츠의 세로 너비가 그리드 컨테이너(Container)보다 작아야 합니다.


값	|| 의미	|| 기본값
normal	|| stretch와 같습니다.	|| normal
start	|| 시작점(위쪽) 정렬	
center	|| 수직 가운데 정렬	
end	|| 끝점(아래쪽) 정렬	
space-around	|| 각 행 위아래에 여백을 고르게 정렬	
space-between	|| 첫 행은 시작점에, 끝 행은 끝점에 정렬되고 나머지 여백으로 고르게 정렬	
space-evenly	|| 모든 여백을 고르게 정렬	
stretch	|| 열 축을 채우기 위해 그리드 콘텐츠를 늘림


```JavaScript

.container {
  width: 450px;
  height: 450px;
  display: grid;
  grid-template-rows: repeat(3, 100px);
  grid-template-columns: repeat(3, 100px);
  align-content: <align-content>;
}

```

### justify-content

- 그리드 콘텐츠(Contents)를 수평(행 축) 정렬합니다.
그리드 콘텐츠의 가로 너비가 그리드 컨테이너(Container)보다 작아야 합니다.



값	|| 의미	|| 기본값
normal	|| stretch와 같습니다.	|| normal
start	|| 시작점(왼쪽) 정렬	
center	|| 수평 가운데 정렬	
end	|| 끝점(오른쪽) 정렬	
space-around	|| 각 열 좌우에 여백을 고르게 정렬	
space-between	|| 첫 열은 시작점에, 끝 열은 끝점에 정렬되고 나머지 여백으로 고르게 정렬	
space-evenly	|| 모든 여백을 고르게 정렬	
stretch	|| 행 축을 채우기 위해 그리드 콘텐츠를 늘림


```JavaScript

.container {
  width: 450px;
  height: 450px;
  display: grid;
  grid-template-rows: repeat(3, 100px);
  grid-template-columns: repeat(3, 100px);
  justify-content: <justify-content>;
}

```


### place-content

- align-content와 justify-content의 단축 속성입니다.
하나의 값만 입력하면 두 속성에 모두 적용됩니다.


```JavaScript

.container {
  place-content: <align-content> <justify-content>;
}

```

### align-items

- 그리드 아이템(Items)들을 수직(열 축) 정렬합니다.
그리드 아이템의 세로 너비가 자신이 속한 그리드 행(Track)의 크기보다 작아야 합니다.

값	|| 의미	|| 기본값
normal	|| stretch와 같습니다.	|| normal
start	|| 시작점(위쪽) 정렬	
center	|| 수직 가운데 정렬	
end	|| 끝점(아래쪽) 정렬	
stretch	|| 열 축을 채우기 위해 그리드 아이템을 늘림	


```JavaScript

.container {
  width: 450px;
  height: 450px;
  display: grid;
  grid-template-rows: repeat(3, 1fr);
  grid-template-columns: repeat(3, 1fr);
  align-items: <align-items>;
}

```

### justify-items

- 그리드 아이템(Items)들을 수평(행 축) 정렬합니다.
그리드 아이템의 가로 너비가 자신이 속한 그리드 열(Track)의 크기보다 작아야 합니다.


값	|| 의미	|| 기본값
normal	|| stretch와 같습니다.	|| normal
start	|| 시작점(왼쪽) 정렬	
center	|| 수평 가운데 정렬	
end	|| 끝점(오른쪽) 정렬	
stretch	|| 행 축을 채우기 위해 그리드 아이템을 늘림	


```JavaScript

.container {
  width: 450px;
  height: 450px;
  display: grid;
  grid-template-rows: repeat(3, 1fr);
  grid-template-columns: repeat(3, 1fr);
  justify-items: <justify-items>;
}

```

### place-items

- align-items와 justify-items의 단축 속성입니다.
하나의 값만 입력하면 두 속성에 모두 적용됩니다.



```JavaScript

.container {
  place-items: <align-items> <justify-items>;
}

```














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


### grid-row-start

- 그리드 아이템(Item)을 배치하기 위해 그리드 선(Line)의 ‘시작 위치’와 ‘끝 위치’를 지정합니다.
‘숫자’를 지정하거나, ‘선 이름’을 지정하거나, span 키워드를 사용합니다.

```JavaScript

.container {
  display: grid;
  grid-template-rows: repeat(2, 1fr);
  grid-template-columns: repeat(3, 1fr);
}
.item:nth-child(1) {
  grid-row-start: 1;
  grid-row-end: 3;
  grid-column-start: 2;
  grid-column-end: 4;
}

```

### grid-row-end

- 그리드 아이템(Item)을 배치하기 위해 그리드 선(Line)의 ‘시작 위치’와 ‘끝 위치’를 지정합니다.
‘숫자’를 지정하거나, ‘선 이름’을 지정하거나, span 키워드를 사용합니다.



### grid-row

- grid-row-start과 grid-row-end의 단축 속성입니다.
각 속성을 /로 구분하는 것에 주의하세요.


```JavaScript

.item {
  grid-row: <grid-row-start> / <grid-row-end>;
}

```

### grid-column-start

- 그리드 아이템(Item)을 배치하기 위해 그리드 선(Line)의 ‘시작 위치’와 ‘끝 위치’를 지정합니다.
‘숫자’를 지정하거나, ‘선 이름’을 지정하거나, span 키워드를 사용합니다.


### grid-column-end

- 그리드 아이템(Item)을 배치하기 위해 그리드 선(Line)의 ‘시작 위치’와 ‘끝 위치’를 지정합니다.
‘숫자’를 지정하거나, ‘선 이름’을 지정하거나, span 키워드를 사용합니다.

### grid-column

- grid-column-start과 grid-column-end의 단축 속성입니다.
각 속성을 /로 구분하는 것에 주의하세요.


```JavaScript

.item {
  grid-column: <grid-column-start> / <grid-column-end>;
}

```

### grid-area

- grid-row-start, grid-column-start, grid-row-end 그리고 grid-column-end의 단축 속성입니다.
혹은 grid-template-areas가 참조할 영역(Area) 이름을 설정할 수도 있습니다.
영역 이름을 설정할 경우 grid-row와 grid-column 개념은 무시됩니다.

```JavaScript

.item {
  grid-area: <grid-row-start> / <grid-column-start> / <grid-row-end> / <grid-column-end>;
  grid-area: 영역이름;
}

```

### align-self

- 단일 그리드 아이템(Item)을 수직(열 축) 정렬합니다.
그리드 아이템의 세로 너비가 자신이 속한 그리드 행(Track)의 크기보다 작아야 합니다.

값	|| 의미	|| 기본값
normal	|| stretch와 같습니다.	|| normal
start	|| 시작점(위쪽) 정렬	
center	|| 수직 가운데 정렬	
end	|| 끝점(아래쪽) 정렬	
stretch	|| 열 축을 채우기 위해 그리드 아이템을 늘림

```JavaScript

.container {
  display: grid;
  grid-template-rows: repeat(2, 1fr);
  grid-template-columns: repeat(2, 1fr);
}
.item:nth-child(1) { align-self: start; }
.item:nth-child(2) { align-self: center; }
.item:nth-child(3) { align-self: end; }
.item:nth-child(4) { align-self: stretch; }

```

### justify-self

- 단일 그리드 아이템(Item)을 수평(행 축) 정렬합니다.
그리드 아이템의 가로 너비가 자신이 속한 그리드 열(Track)의 크기보다 작아야 합니다.


값	|| 의미	|| 기본값
normal	|| stretch와 같습니다.	|| normal
start	|| 시작점(왼쪽) 정렬	
center	|| 수평 가운데 정렬	
end	|| 끝점(오른쪽) 정렬	
stretch	|| 행 축을 채우기 위해 그리드 아이템을 늘림	

```JavaScript

.container {
  display: grid;
  grid-template-rows: repeat(2, 1fr);
  grid-template-columns: repeat(2, 1fr);
}
.item:nth-child(1) { justify-self: start; }
.item:nth-child(2) { justify-self: center; }
.item:nth-child(3) { justify-self: end; }
.item:nth-child(4) { justify-self: stretch; }

```

### place-self

- align-self와 justify-self의 단축 속성입니다.
하나의 값만 입력하면 두 속성에 모두 적용됩니다.

```JavaScript

.item {
  place-self: <align-self> <justify-self>;
}

```

### order

- 그리드 아이템이 자동 배치되는 순서를 변경할 수 있습니다.
숫자가 작을수록 앞서 배치됩니다.


```JavaScript

.container {
  display: grid;
  grid-template-rows: repeat(2, 1fr);
  grid-template-columns: repeat(3, 1fr);
}
.item:nth-child(1) { order: 1; }
.item:nth-child(3) { order: 5; }
.item:nth-child(5) { order: -1; }

```

### z-index

- z-index 속성을 이용해 아이템이 쌓이는 순서를 변경할 수 있습니다.


```JavaScript

.item:nth-child(1) {
  grid-area: 1 / 1 / 2 / 3;
}
.item:nth-child(2) {
  grid-area: 1 / 2 / 3 / 3;
  z-index: 1;
}
.item:nth-child(3) {
  grid-area: 2 / 2 / 3 / 4;
}

```



## Grid Functions

### repeat

### minmax

### fit-content


## Grid Units

### fr


### min-content


### max-content


### auto-fill, auto-fit


## 용어 정리

### Track
- 트랙(Track)은 하나의 행(Row) 혹은 열(Column)을 의미합니다.

### Line
- 선(Line)은 일반적으로 거터(Gutter)라고 하는 트랙과 트랙 사이의 간격을 의미합니다.

### Cell
- 셀(Cell)은 아이템(Item)이 배치되는 최소 단위의 영역(Area)입니다.

### Area
- 영역(Area)은 아이템이 배치되는, 하나 이상의 셀(Cell)로 이루어진 영역입니다.