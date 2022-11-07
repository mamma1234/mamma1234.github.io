---
layout: post
title: 'javascirpt function'
description:
headline:
modified: 2022-11-07
category: webdevelopment
imagefeature:
tags: [javascript function]
mathjax:
chart:
share: true
comments: true
featured: true
disqus:
---

# Record

## 목차

-   [](#)
-   [개념](#개념)

## 개념

### function 키워드를 사용하지 말자

-   함수를 쓰고자 할때는 arraw함수
-   생성자함수로 쓰고자 할때는 Class
-   메소드로 쓰고자 할때 method 축약형

```javascript

    cost obj = {
        name:'name',
        methos() {
            console.log(this.name);
        }
    }
```

-   generator 를 쓸 경우는 function\*
    -   제너레이터 함수는 사용자의 요구에 따라 (yield와 next를 통해) 일시적으로 정지될 수도 있고, 다시 시작될 수도 있다.
