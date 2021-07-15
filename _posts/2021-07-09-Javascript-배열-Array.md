---
layout: post
title: "Javascript-배열-Array"
description: 
headline: 
modified: 2021-07-09
category: webdevelopment
imagefeature: cover3.jpg
tags: [Javascript-배열-Array]
mathjax: 
chart: 
share: true
comments: true
featured: true
disqus:
---

# Record
## 개념
- 자료구조

## 목차
- [forEach](#forEach)
- [RN flex](#rn-flex)
- [component](#component)
    - [View](#view)


### forEach
- thisArg 매개변수(this)를 forEach()에 제공했기에, callback은 전달받은 this의 값을 자신의 this 값으로 사용할 수 있습니다. 
    - arr.forEach(callback(currentvalue[, index[, array]])[, thisArg])
```JavaScript
fruits.forEach((fruit) => console.log(fruit, second), second);
````
