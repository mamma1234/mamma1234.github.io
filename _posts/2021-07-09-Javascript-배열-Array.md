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
- [find](#find)
- [component](#component)
    - [View](#view)


### forEach
- thisArg 매개변수(this)를 forEach()에 제공했기에, callback은 전달받은 this의 값을 자신의 this 값으로 사용할 수 있습니다. 
    - arr.forEach(callback(currentvalue[, index[, array]])[, thisArg])
```JavaScript
fruits.forEach((fruit) => console.log(fruit, second), second);
```

### find
```JavaScript
const fruits =  ['1', '2', '1']
const findedata= fruits.find((value, index)=>
    value === '1'
)
console.log(findedata);

$1
```

### filter
```JavaScript
const fruits =  ['1', '2', '1']
const findedata= fruits.filter((value, index)=>
    value === '1'
)
console.log(findedata);

$[ '1', '1' ]
```

### map
```JavaScript
const fruits =  ['1', '2', '1']
const findedata2= fruits.map((value, index)=>
    value + 333
)
console.log(findedata2);

$[ '1333', '2333', '1333' ]
```
