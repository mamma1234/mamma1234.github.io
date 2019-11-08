---
layout: post
title: "ES6"
description: 
headline: 
modified: 2019-11-08
category: webdevelopment
imagefeature: cover3.jpg
tags: [ES6]
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

### ES6 에서 사용하는 변수 선언. ES5 에서 사용하던 var 외에 const나 let
- 블록 스코프 변수인 let은 자신을 정의한 블록에서만 접근 가능하다.
- const 담긴 값이 불변을 뜻하는게 아니라, 단지 변수의 식별자가 재할당 될 수 없다.
``` 
const ME = { "name": "ES6" } 
console.log(ME.name); //ES6 
ME.name = "ES7"; 
console.log(ME.name); //ES7, 객체 값 재할당 
ME = {}; //변수 자체는 상수값으로 수정되지 않는다. 
console.log(ME); //{ name: 'ES7' }
```


### module import, export
- import - 다른 스크립트의 특정 함수, 객체, primitives를 사용하기 위해 들여오는 키워드
``` 
import * as name from "module-name"; 
import { member as alias } from "module-name"; 
import { member1 , member2 } from "module-name"; 
import { member1 , member2 as alias2 , [...] } from "module-name"; 
import defaultMember, { member [ , [...] ] } from "module-name"; 
import defaultMember, * as name from "module-name"; 
import "module-name";
``` 

- export - 반대로 스크립트 내의 특정 함수, 객체, primitives를 내보내는 키워드
``` 
export { variable1 as name1, variable2 as name2, …, nameN };
export let name1, name2, …, nameN; 
export let name1 = …, name2 = …, …, nameN; 
export { name1 as default, … }; 
export * from …; export { name1, name2, …, nameN } from …;
export { import1 as name1, import2 as name2, …, nameN } from …;
``` 

- default를 사용한 export와 import

### arrow function
- 기존의 function보다 빠르며 간결한 구문을 보여주는 함수이다.
- 한줄 코드인경우 return 구문없이 자동으로 반환된다
- 항상 익명함수이다.
- 생성자를 사용할 수 없다.
``` 
var plus = function(a, b) { var result = a + b; return result; }
let plus = (a, b) => { let result = a + b; return result; }
``` 
``` 
var result = function(a, b) { return a * b; } 
var result2 = (a, b) => a * b;
``` 
``` 
- this 사용 범위
- 화살표 함수의 this는 외부함수(부모함수)의 this를 상속받기 때문에 this는 항상 일정하다.
function phone() { 
    var self = this,
    name = "Galaxy s", 
    version = 6;             
    versionUp = function() { console.log(this); self.version++; }; 
}
function phone(){ 
    this.sName = "Galaxy s"; 
    this.sVersion = 0; 
    test => { console.log(this); this.version++; }; 
}
``` 

### 템플릿 리터럴 (Template Literals)
- 역 따옴표(backticks)을 사용하여 문자열을 연결하거나 문자열 중간에 변수를 삽입하여 사용할 수 있다.
또한 ${}에는 값을 만들어내는 자바스크립트 식이라면 어떤 것이든 들어갈 수 있다.

let message = ``Hello ${student.name} from ${student.city}``;
