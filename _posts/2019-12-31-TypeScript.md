---
layout: post
title: "TypeScript (미완성)"
description: 
headline: 
modified: 2019-12-31
category: development
imagefeature: cover3.jpg
tags: [TypeScript]
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

## 특징
- 자바스크립트의 태생적 문제를 극복하고자 CoffeeScript, Dart, Haxe와 같은 AltJS(자바스크립트의 대체 언어)가 등장하였다.

TypeScript 또한 자바스크립트 대체 언어의 하나로써 자바스크립트(ES5)의 Superset(상위확장)이다. C#의 창시자인 덴마크 출신 소프트웨어 엔지니어 Anders Hejlsberg(아네르스 하일스베르)가 개발을 주도한 TypeScript는 Microsoft에서 2012년 발표한 오픈소스로, 정적 타이핑을 지원하며 ES6(ECMAScript 2015)의 클래스, 모듈 등과 ES7의 Decorator 등을 지원한다.

TypeScript는 ES5의 Superset이므로 기존의 자바스크립트(ES5) 문법을 그대로 사용할 수 있다. 또한, ES6의 새로운 기능들을 사용하기 위해 Babel과 같은 별도 트랜스파일러(Transpiler)를 사용하지 않아도 ES6의 새로운 기능을 기존의 자바스크립트 엔진(현재의 브라우저 또는 Node.js)에서 실행할 수 있다.

## 설치
npm install -g typescript
tsc -v

## 트랜스파일링
tsc person (person.tx)
==> person.js (ES3)

tsc person -t es6 (ES3, ES5, ES6(ES2015), ES2016, ES2017(ESNext))

tsc person student

tsc *.ts

## 실행
node person
node student

## 감지
- --watch 또는 -w 옵션을 사용하면 트랜스파일링 대상 파일의 내용이 변경되었을 때 이를 감지하여 자동으로 트랜스파일링이 실행된다.
tsc student --watch


## tsconfig.json
- TypeScript를 위한 프로젝트 단위의 환경 파일로써 컴파일 옵션과 컴파일 대상에 대한 설정 등을 기술한 것

```
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "sourceMap": true
  }
}
```

- files 프로퍼티에는 컴파일 대상 파일의 상대 경로 또는 절대 경로를 명시적으로 설정한다.
```
{
  "files": [
    "src/file1.ts",
    "src/file2.ts"
  ]
}
```

- include 프로퍼티에는 컴파일 대상 파일 리스트를 설정한다. exclude 프로퍼티에는 컴파일 대상에서 제외할 파일 리스트를 설정한다.
```
{
  "include": [
    "src/**/*"
  ],
  "exclude": [
    "node_modules",
    "**/*.spec.ts"
  ]
}
```

- src/\*\*/\*는 src 폴더 내에 있는 모든 서브 폴더 내의 모든 파일(.ts, .tsx)을 의미한다. 컴파일 옵션 "allowJs": true를 설정하면 .js와 .jsx 파일도 컴파일 대상이 된다.
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "sourceMap": true
  }
}

## 타입 선언 (Type Declaration)
### 정적 타이핑 (Static Typing)
- C나 Java같은 C-family 언어는 변수를 선언할 때 변수에 할당할 값의 타입에 따라 사전에 타입을 명시적으로 선언(Type declaration)하여야 하며 선언한 타입에 맞는 값을 할당해야 한다. 이를 정적 타이핑(Static Typing)이라 한다.
### 동적 타이핑 (Dynamic Typing)
- 자바스크립트는 동적 타입(dynamic typed) 언어 혹은 느슨한 타입(loosely typed) 언어이다. 이것은 변수의 타입 선언 없이 값이 할당되는 과정에서 동적으로 타입을 추론(Type Inference)한다는 의미이다. 동적 타입 언어는 타입 추론에 의해 변수의 타입이 결정된 후에도 같은 변수에 여러 타입의 값을 교차하여 할당할 수 있다
### 타입 추론
- 약 타입 선언을 생략하면 값이 할당되는 과정에서 동적으로 타입이 결정된다. 이를 타입 추론(Type Inference)이라 한다.

<pre><code>
```
// 변수 foo는 string 타입이다.
let foo: string = 'hello';
let bar: number = 1;
let bar: number = true; // error TS2322: Type 'true' is not assignable to type 'number'.

// 함수선언식
function multiply1(x: number, y: number): number {
  return x * y;
}

// 함수표현식
const multiply2 = (x: number, y: number): number => x * y;


// boolean
let isDone: boolean = false;

// null
let n: null = null;

// undefined
let u: undefined = undefined;

// number
let decimal: number = 6;
let hex: number = 0xf00d;
let binary: number = 0b1010;
let octal: number = 0o744;

// string
let color: string = "blue";
color = 'red';
let myName: string = `Lee`; // ES6 템플릿 문자열
let greeting: string = `Hello, my name is ${ myName }.`; // ES6 템플릿 대입문

// object
const obj: object = {};

// array
let list1: any[] = [1, 'two', true];
let list2: number[] = [1, 2, 3];
let list3: Array<number> = [1, 2, 3]; // 제네릭 배열 타입

// tuple : 고정된 요소수 만큼의 타입을 미리 선언후 배열을 표현
let tuple: [string, number];
tuple = ['hello', 10]; // OK
tuple = [10, 'hello']; // Error
tuple = ['hello', 10, 'world', 100]; // Error
tuple.push(true); // Error

// enum : 열거형은 숫자값 집합에 이름을 지정한 것이다.
enum Color1 {Red, Green, Blue};
let c1: Color1 = Color1.Green;

console.log(c1); // 1

enum Color2 {Red = 1, Green, Blue};
let c2: Color2 = Color2.Green;

console.log(c2); // 2

enum Color3 {Red = 1, Green = 2, Blue = 4};
let c3: Color3 = Color3.Blue;

console.log(c3); // 4

/*
any: 타입 추론(type inference)할 수 없거나 타입 체크가 필요 없는 변수에 사용한다.
var 키워드로 선언한 변수와 같이 어떤 타입의 값이라도 할당할 수 있다.
*/
let notSure: any = 4;
notSure = 'maybe a string instead';
notSure = false; // okay, definitely a boolean

// void : 일반적으로 함수에서 반환값이 없을 경우 사용한다.
function warnUser(): void {
  console.log("This is my warning message");
}

// never : 결코 발생하지 않는 값
function infiniteLoop(): never {
  while (true) {}
}

function error(message: string): never {
  throw new Error(message);
}
```
</code></pre>



## 클래스
### 클래스 정의 (Class Definition)
- ES6 클래스는 클래스 몸체에 메소드만을 포함할 수 있다. 클래스 몸체에 클래스 프로퍼티를 선언할 수 없고 반드시 생성자 내부에서 클래스 프로퍼티를 선언하고 초기화한다.

Typescript 클래스는 클래스 몸체에 클래스 프로퍼티를 사전 선언하여야 한다.

<code>
// ES6
class Person {
  constructor(name) {
    // 클래스 프로퍼티의 선언과 초기화
    this.name = name;
  }

  walk() {
    console.log(`${this.name} is walking.`);
  }
}

// Typescript
class Person {
  // 클래스 프로퍼티를 사전 선언하여야 한다
  name: string;

  constructor(name: string) {
    // 클래스 프로퍼티수에 값을 할당
    this.name = name;
  }

  walk() {
    console.log(`${this.name} is walking.`);
  }
}
</code>

### 접근 제한자
<code>
class Foo {
  public x: string;
  protected y: string;
  private z: string;

  constructor(x: string, y: string, z: string) {
    // public, protected, private 접근 제한자 모두 클래스 내부에서 참조 가능하다.
    this.x = x;
    this.y = y;
    this.z = z;
  }
}

const foo = new Foo('x', 'y', 'z');

// public 접근 제한자는 클래스 인스턴스를 통해 클래스 외부에서 참조 가능하다.
console.log(foo.x);

// protected 접근 제한자는 클래스 인스턴스를 통해 클래스 외부에서 참조할 수 없다.
console.log(foo.y);
// error TS2445: Property 'y' is protected and only accessible within class 'Foo' and its subclasses.

// private 접근 제한자는 클래스 인스턴스를 통해 클래스 외부에서 참조할 수 없다.
console.log(foo.z);
// error TS2341: Property 'z' is private and only accessible within class 'Foo'.

class Bar extends Foo {
  constructor(x: string, y: string, z: string) {
    super(x, y, z);

    // public 접근 제한자는 자식 클래스 내부에서 참조 가능하다.
    console.log(this.x);

    // protected 접근 제한자는 자식 클래스 내부에서 참조 가능하다.
    console.log(this.y);

    // private 접근 제한자는 자식 클래스 내부에서 참조할 수 없다.
    console.log(this.z);
    // error TS2341: Property 'z' is private and only accessible within class 'Foo'.
  }
}
</code>