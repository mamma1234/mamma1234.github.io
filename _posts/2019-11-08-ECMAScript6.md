---
layout: post
title: 'ES6'
description:
headline:
modified: 2019-11-08
category: Laguage
imagefeature:
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

## 목차

-   [ES6 에서 사용하는 변수 선언. ES5 에서 사용하던 var 외에 const나 let](#)
-   [module import, export](#)
-   [arrow function](#)
-   [템플릿 리터럴 (Template Literals)](#)
-   [개선된 객체 리터럴 (Enhanced Object Literal)](#)
-   [스프레드 연산자 Spread Operator](#)
-   [프라미스 Promise](#)
-   [Fetch API](#)
-   [클래스 (Class)](#)
-   [팁](#)
    -   [Nullish Coalescing Operator](#)
    -   [Object Destructuring](#)
    -   [Spread Syntax Object](#)
    -   [Spread Syntax Array](#)
    -   [Optional Chaining](#)
    -   [Template Literals](#)
    -   [Promise -> Async/await](#)

### ES6 에서 사용하는 변수 선언. ES5 에서 사용하던 var 외에 const나 let

-   블록 스코프 변수인 let은 자신을 정의한 블록에서만 접근 가능하다.
-   const 담긴 값이 불변을 뜻하는게 아니라, 단지 변수의 식별자가 재할당 될 수 없다.

```
const ME = { "name": "ES6" }
console.log(ME.name); //ES6
ME.name = "ES7";
console.log(ME.name); //ES7, 객체 값 재할당
ME = {}; //변수 자체는 상수값으로 수정되지 않는다.
console.log(ME); //{ name: 'ES7' }
```

### module import, export

-   import - 다른 스크립트의 특정 함수, 객체, primitives를 사용하기 위해 들여오는 키워드

```
import * as name from "module-name";
import { member as alias } from "module-name";
import { member1 , member2 } from "module-name";
import { member1 , member2 as alias2 , [...] } from "module-name";
import defaultMember, { member [ , [...] ] } from "module-name";
import defaultMember, * as name from "module-name";
import "module-name";
```

-   export - 반대로 스크립트 내의 특정 함수, 객체, primitives를 내보내는 키워드

```
export { variable1 as name1, variable2 as name2, …, nameN };
export let name1, name2, …, nameN;
export let name1 = …, name2 = …, …, nameN;
export { name1 as default, … };
export * from …; export { name1, name2, …, nameN } from …;
export { import1 as name1, import2 as name2, …, nameN } from …;
```

-   default를 사용한 export와 import

### arrow function

-   기존의 function보다 빠르며 간결한 구문을 보여주는 함수이다.
-   한줄 코드인경우 return 구문없이 자동으로 반환된다
-   항상 익명함수이다.
-   생성자를 사용할 수 없다.

```
var plus = function(a, b) { var result = a + b; return result; }
let plus = (a, b) => { let result = a + b; return result; }
```

```
var result = function(a, b) { return a * b; }
var result2 = (a, b) => a * b;
```

-   this 사용 범위
-   화살표 함수의 this는 외부함수(부모함수)의 this를 상속받기 때문에 this는 항상 일정하다.

```
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

-   역 따옴표(backticks)을 사용하여 문자열을 연결하거나 문자열 중간에 변수를 삽입하여 사용할 수 있다.
-   또한 ${}에는 값을 만들어내는 자바스크립트 식이라면 어떤 것이든 들어갈 수 있다.

let message = '`Hello ${student.name} from ${student.city}'`;

### 개선된 객체 리터럴 (Enhanced Object Literal)

```
// ES5
var skier = {
  name: name,
  sound: sound,
  powderYell: function() {
    var yell = this.sound.toUpperCase();
    console.log(yell + yell + yell + '!!!');
  }
  speed: function(mph) {
    this.speed = mph;
    console.log('속력(mph):', mph);
  }
}

// ES6
let skier = {
  name,
  sound,
  powderYell() {
    let yell = this.sound.toUpperCase();
    console.log(`${yell} ${yell} ${yell}!!!`);
  }
  speed(mph) {
    this.speed = mph;
    console.log('속력(mph):', mph);
  }
}
```

### 스프레드 연산자 Spread Operator

-   스프레드 연산자는 ... 세개의 점으로 이루어진 연산자로, 몇 가지 다른 역할을 담당한다.
-   Spread 연산자는 연산자의 대상 배열 또는 이터러블(iterable)을 "개별" 요소로 분리한다.

```
개별 요소로 분리
// 배열
console.log(...[1, 2, 3]); // -> 1, 2, 3
// 문자열
console.log(...'Helllo');  // H e l l l o
// Map과 Set
console.log(...new Map([['a', '1'], ['b', '2']]));  // [ 'a', '1' ] [ 'b', '2' ]
console.log(...new Set([1, 2, 3]));  // 1 2 3
```

-   함수의 파라미터로 사용하는 방법

```
// ES6
function foo(x, y, z) {
  console.log(x); // 1
  console.log(y); // 2
  console.log(z); // 3
}
const arr = [1, 2, 3];
foo(...arr);// Array를 받아서 각 매개변수로 전달되었다.
```

-   배열에서 사용하는 방법

```
가독성up
// ES6
const arr = [1, 2, 3];
// ...arr은 [1, 2, 3]을 개별 요소로 분리한다
console.log([...arr, 4, 5, 6]); // [ 1, 2, 3, 4, 5, 6 ]

// ES6
const arr1 = [1, 2, 3];
const arr2 = [4, 5, 6];

// ...arr2는 [4, 5, 6]을 개별 요소로 분리한다
arr1.push(...arr2); // == arr1.push(4, 5, 6);
console.log(arr1); // [ 1, 2, 3, 4, 5, 6 ]
```

-   객체에서 사용하기

```
const o1 = { x: 1, y: 2 };
const o2 = { ...o1, z: 3 };
console.log(o2); // { x: 1, y: 2, z: 3 }

const target = { x: 1, y: 2 };
const source = { z: 3 };
// Object.assign를 사용하여도 동일한 작업을 할 수 있다.
// Object.assign은 타깃 객체를 반환한다
console.log(Object.assign(target, source)); // { x: 1, y: 2, z: 3 }
```

### 프라미스 Promise

-   비동기 프라미스 만들기

```
function myAsyncFunction(url) {
  return new Promise((resolve, reject) => {
    const xhr = new XMLHttpRequest();
    xhr.open("GET", url);
    xhr.onload = () => resolve(xhr.responseText);
    xhr.onerror = () => reject(xhr.statusText);
    xhr.send();
  });
}

myAsyncFunction('https://jsonplaceholder.typicode.com/todos/1').then(
  json => console.log(json),
  err => console.log(new Error('조회 실패'))
)
```

### Fetch API

-   Fetch API를 이용하면 Request나 Resposne와 같은 HTTP의 파이프라인을 구성하는 요소를 조작하는것이 가능하다. 또한 fetch() 메서드를 이용하여 비동기 네트워크 통신을 알기쉽게 기술할 수 있다. fetch는 이전에 제공하던 XMLHttpRequest 대체제이다.

```
var xhr = new XMLHttpRequest(); // Set up our HTTP request
// Setup our listener to process compeleted requests
xhr.onreadystatechange = function () {
    // Only run if the request is complete
    if (xhr.readyState !== 4) return;
    // Process our return data
    if (xhr.status >= 200 && xhr.status < 300) {
        // What do when the request is successful
        console.log(JSON.parse(xhr.responseText));
    }
};
xhr.open('GET', 'https://jsonplaceholder.typicode.com/posts');
xhr.send();

fetch('https://jsonplaceholder.typicode.com/posts')
    .then(function (response) {
        return response.json();
    })
    .then(function (data) {
        console.log(data);
    });
```

### 클래스 (Class)

-   이전 자바스크립트에는 공식적으로 클래스가 없어서 프로토타입을 사용해 구현하였지만, ES6에는 클래스 선언이 추가되었다.

```
// ES5
function Vacation(destination, length) {
  this.destination = destination;
  this.length = length;
}

Vacation.prototype.print = function() {
  console.log(this.destination + "은(는) " + this.length + "일 걸립니다");
}

var trip = new Vacation("마우이", 7);
trip.print() // 마우이은(는) 7일 걸립니다.

// ES6
class Vacation {
  constructor(destination, length) {
    this.destination = destination;
    this.length = length;
  }

  print() {
    console.log(this.destination + "은(는) " + this.length + "일 걸립니다");
  }
}

const trip = new Vacation("칠레", 7);
trip.print() // 칠레은(는) 7일 걸립니다.
```

-   extends를 이용한 클래스 확장

```
//상속
class Expedition extends Vacation {
  constructor(destination, length, gear) {
    super(destination, length);
    this.gear = gear;
  }

  print() {
    super.print();
    console.log(`당신의 ${this.gear.join("와(과) 당신의 ")}를(을) 가져오십시오.`);
  }
}

const trip = new Expedition("한라산", 3, ["선글라스", "배낭", "카메라"]);
trip.print();
// 한라산은(는) 3일 걸립니다.
// 당신의 선글라스와(과) 당신의 배낭와(과) 당신의 카메라를(을) 가져오십시오.
```

### 팁

#### Nullish Coalescing Operator

```JavaScript
// Nullish coalescing operator
function printMessage(text) {
  const message = text ?? 'Nothing to display';
  console.log(message);
}

printMessage('Hello');
printMessage(null); ==> 'Nothing to display'
printMessage(undefined); ==> 'Nothing to display'


// 🚨 Default parameter is only for undefined
function printMessage(text = 'Nothing to display 😜') {
  console.log(text);
}




// 🚨 Logical OR operator ||
function printMessage(text) {
  const message = text || 'Nothing to display 😜';
  console.log(message);
}


printMessage('Hello');
printMessage(null); ==> 'Nothing to display'
printMessage(undefined); ==> 'Nothing to display'
printMessage(0); ==> 'Nothing to display'
printMessage(''); ==> 'Nothing to display'
```

#### Object Destructuring

```JavaScript
  const { name, age } = person;
```

#### Spread Syntax Object

```JavaScript
const item = { type: '👔', size: 'M' };
const detail = { price: 20, made: 'Korea', gender: 'M' };

// ✅ Good Code ✨
const shirt0 = Object.assign(item, detail);
console.log(shirt0);

// ✅ Better! Code ✨
const shirt = { ...item, ...detail, price: 30 };
console.log(shirt);

```

#### Spread Syntax Array

```JavaScript
let fruits = ['🍉', '🍊', '🍌'];
const fruits2 = ['🍈', '🍑', '🍍'];

let combined = fruits.concat(fruits2);
combined = [...fruits, '🍒', ...fruits2];

```

#### Optional Chaining

```JavaScript
// Optional Chaining
const bob = {
  name: 'Julia',
  age: 20,
};
const anna = {
  name: 'Julia',
  age: 20,
  job: {
    title: 'Software Engineer',
  },
};

// ❌ Bad Code 💩
function displayJobTitle(person) {
  if (person.job && person.job.title) {
    console.log(person.job.title);
  }
}

// ✅ Good Code ✨
function displayJobTitle(person) {
  if (person.job?.title) {
    console.log(person.job.title);
  }
}

// ✅ Good Code ✨
function displayJobTitle(person) {
  const title = person.job?.title ?? 'No Job Yet 🔥';
  console.log(title);
}

displayJobTitle(bob); ==> 'No Job Yet 🔥'
displayJobTitle(anna); ==> 'Software Engineer'

```

#### Template Literals

```JavaScript
// ❌ Bad Code 💩
console.log(
  'Hello ' + person.name + ', Your current score is: ' + person.score
);

// ✅ Good Code ✨
console.log(`Hello ${person.name}, Your current score is: ${person.score}`);

```

#### Promise -> Async/await

```JavaScript

// Promise -> Async/await

// ❌ Bad Code 💩
function displayUser() {
  fetchUser() //
    .then((user) => {
      fetchProfile(user) //
        .then((profile) => {
          updateUI(user, profile);
        });
    });
}

// ✅ Good Code ✨
async function displayUser() {
  const user = await fetchUser();
  const profile = await fetchProfile(user);
  updateUI(user, profile);
}
```
