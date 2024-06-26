---
layout: post
title: 'TypeScript'
description:
headline:
modified: 2019-12-31
category: development
imagefeature:
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

-   자바스크립트의 태생적 문제를 극복하고자 CoffeeScript, Dart, Haxe와 같은 AltJS(자바스크립트의 대체 언어)가 등장하였다.

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

tsc \*.ts

## 실행

node person
node student

## 감지

-   --watch 또는 -w 옵션을 사용하면 트랜스파일링 대상 파일의 내용이 변경되었을 때 이를 감지하여 자동으로 트랜스파일링이 실행된다.
    tsc student --watch

## tsconfig.json

-   TypeScript를 위한 프로젝트 단위의 환경 파일로써 컴파일 옵션과 컴파일 대상에 대한 설정 등을 기술한 것

```
{
  "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "sourceMap": true
  }
}
```

-   files 프로퍼티에는 컴파일 대상 파일의 상대 경로 또는 절대 경로를 명시적으로 설정한다.

```
{
  "files": [
    "src/file1.ts",
    "src/file2.ts"
  ]
}
```

-   include 프로퍼티에는 컴파일 대상 파일 리스트를 설정한다. exclude 프로퍼티에는 컴파일 대상에서 제외할 파일 리스트를 설정한다.

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

-   src/\*\*/\*는 src 폴더 내에 있는 모든 서브 폴더 내의 모든 파일(.ts, .tsx)을 의미한다. 컴파일 옵션 "allowJs": true를 설정하면 .js와 .jsx 파일도 컴파일 대상이 된다.
    {
    "compilerOptions": {
    "target": "es5",
    "module": "commonjs",
    "sourceMap": true
    }
    }

## 타입 선언 (Type Declaration)

### 정적 타이핑 (Static Typing)

-   C나 Java같은 C-family 언어는 변수를 선언할 때 변수에 할당할 값의 타입에 따라 사전에 타입을 명시적으로 선언(Type declaration)하여야 하며 선언한 타입에 맞는 값을 할당해야 한다. 이를 정적 타이핑(Static Typing)이라 한다.

### 동적 타이핑 (Dynamic Typing)

-   자바스크립트는 동적 타입(dynamic typed) 언어 혹은 느슨한 타입(loosely typed) 언어이다. 이것은 변수의 타입 선언 없이 값이 할당되는 과정에서 동적으로 타입을 추론(Type Inference)한다는 의미이다. 동적 타입 언어는 타입 추론에 의해 변수의 타입이 결정된 후에도 같은 변수에 여러 타입의 값을 교차하여 할당할 수 있다

### 타입 추론

-   약 타입 선언을 생략하면 값이 할당되는 과정에서 동적으로 타입이 결정된다. 이를 타입 추론(Type Inference)이라 한다.

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

## 클래스

### 클래스 정의 (Class Definition)

-   ES6 클래스는 클래스 몸체에 메소드만을 포함할 수 있다. 클래스 몸체에 클래스 프로퍼티를 선언할 수 없고 반드시 생성자 내부에서 클래스 프로퍼티를 선언하고 초기화한다.

Typescript 클래스는 클래스 몸체에 클래스 프로퍼티를 사전 선언하여야 한다.

<pre><code>

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

</code></pre>

### 접근 제한자

<code>
```
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

class Foo {
/_
접근 제한자가 선언된 생성자 파라미터 x는 클래스 프로퍼티로 선언되고 지동으로 초기화된다.
public이 선언되었으므로 x는 클래스 외부에서도 참조가 가능하다.
_/
constructor(public x: string) { }
}

const foo = new Foo('Hello');
console.log(foo); // Foo { x: 'Hello' }
console.log(foo.x); // Hello

```
</code>


### readonly
- Typescript는 readonly 키워드를 사용할 수 있다. readonly가 선언된 클래스 프로퍼티는 선언 시 또는 생성자 내부에서만 값을 할당할 수 있다. 그 외의 경우에는 값을 할당할 수 없고 오직 읽기만 가능한 상태가 된다. 이를 이용하여 상수의 선언에 사용한다.

<code>
class Foo {
  private readonly MAX_LEN: number = 5;
  private readonly MSG: string;

  constructor() {
    this.MSG = 'hello';
  }

  log() {
    // readonly가 선언된 프로퍼티는 재할당이 금지된다.
    this.MAX_LEN = 10; // Cannot assign to 'MAX_LEN' because it is a constant or a read-only property.
    this.MSG = 'Hi'; // Cannot assign to 'MSG' because it is a constant or a read-only property.

    console.log(`MAX_LEN: ${this.MAX_LEN}`); // MAX_LEN: 5
    console.log(`MSG: ${this.MSG}`); // MSG: hello
  }
}

new Foo().log();
</code>

### static

- ES6 클래스에서 static 키워드는 클래스의 정적(static) 메소드를 정의한다. 정적 메소드는 클래스의 인스턴스가 아닌 클래스 이름으로 호출한다. 따라서 클래스의 인스턴스를 생성하지 않아도 호출할 수 있다.
Typescript에서는 static 키워드를 클래스 프로퍼티에도 사용할 수 있다. 정적 메소드와 마찬가지로 정적 클래스 프로퍼티는 인스턴스가 아닌 클래스 이름으로 호출하며 클래스의 인스턴스를 생성하지 않아도 호출할 수 있다.

```

class Foo {
// 생성된 인스턴스의 갯수
static instanceCounter = 0;
constructor() {
// 생성자가 호출될 때마다 카운터를 1씩 증가시킨다.
Foo.instanceCounter++;
}
}

var foo1 = new Foo();
var foo2 = new Foo();

console.log(Foo.instanceCounter); // 2
console.log(foo2.instanceCounter); // error TS2339: Property 'instanceCounter' does not exist on type 'Foo'.

```


### 추상 클래스
- 추상 클래스(abstract class)는 하나 이상의 추상 메소드를 포함하며 일반 메소드도 포함할 수 있다. 추상 메소드는 내용이 없이 메소드 이름과 타입만이 선언된 메소드를 말하며 선언할 때 abstract 키워드를 사용한다. 추상 클래스를 정의할 때는 abstract 키워드를 사용하며, 직접 인스턴스를 생성할 수 없고 상속만을 위해 사용된다. 추상 클래스를 상속한 클래스는 추상 클래스의 추상 메소드를 반드시 구현하여야 한다.

```

abstract class Animal {
// 추상 메소드
abstract makeSound(): void;
// 일반 메소드
move(): void {
console.log('roaming the earth...');
}
}

// 직접 인스턴스를 생성할 수 없다.
// new Animal();
// error TS2511: Cannot create an instance of the abstract class 'Animal'.

class Dog extends Animal {
// 추상 클래스를 상속한 클래스는 추상 클래스의 추상 메소드를 반드시 구현하여야 한다
makeSound() {
console.log('bowwow~~');
}
}

const myDog = new Dog();
myDog.makeSound();
myDog.move();

```


## 인터페이스
### 변수와 인터페이스

```

// 인터페이스의 정의
interface Todo {
id: number;
content: string;
completed: boolean;
}

// 변수 todo의 타입으로 Todo 인터페이스를 선언하였다.
let todo: Todo;

// 변수 todo는 Todo 인터페이스를 준수하여야 한다.
todo = { id: 1, content: 'typescript', completed: false };

```

### 함수와 인터페이스

```

// 함수 인터페이스의 정의
interface SquareFunc {
(num: number): number;
}

// 함수 인테페이스를 구현하는 함수는 인터페이스를 준수하여야 한다.
const squareFunc: SquareFunc = function (num: number) {
return num \* num;
}

console.log(squareFunc(10)); // 100

```

### 클래스와 인터페이스

```

// 인터페이스의 정의
interface IPerson {
name: string;
sayHello(): void;
}

/_
인터페이스를 구현하는 클래스는 인터페이스에서 정의한 프로퍼티와 추상 메소드를 반드시 구현하여야 한다.
_/
class Person implements IPerson {
// 인터페이스에서 정의한 프로퍼티의 구현
constructor(public name: string) {}

// 인터페이스에서 정의한 추상 메소드의 구현
sayHello() {
console.log(`Hello ${this.name}`);
}
}

function greeter(person: IPerson): void {
person.sayHello();
}

const me = new Person('Lee');
greeter(me); // Hello Lee

```

### 덕 타이핑 (Duck typing)

```

interface IDuck { // 1
quack(): void;
}

class MallardDuck implements IDuck { // 3
quack() {
console.log('Quack!');
}
}

class RedheadDuck { // 4
quack() {
console.log('q~uack!');
}
}

function makeNoise(duck: IDuck): void { // 2
duck.quack();
}

makeNoise(new MallardDuck()); // Quack!
makeNoise(new RedheadDuck()); // q~uack! // 5

(1) 인터페이스 IDuck은 quack 메소드를 정의하였다.

(2) makeNoise 함수는 인터페이스 IDuck을 구현한 클래스의 인스턴스 duck을 인자로 전달받는다.

(3) 클래스 MallardDuck은 인터페이스 IDuck을 구현하였다.

(4) 클래스 RedheadDuck은 인터페이스 IDuck을 구현하지는 않았지만 quack 메소드를 갖는다.

(5) makeNoise 함수에 인터페이스 IDuck을 구현하지 않은 클래스 RedheadDuck의 인스턴스를 인자로 전달하여도 에러 없이 처리된다.

TypeScript는 해당 인터페이스에서 정의한 프로퍼티나 메소드를 가지고 있다면 그 인터페이스를 구현한 것으로 인정한다. 이것을 덕 타이핑(duck typing) 또는 구조적 타이핑(structural typing)이라 한다.

인터페이스를 변수에 사용할 경우에도 덕 타이핑은 적용된다.

interface IPerson {
name: string;
}

function sayHello(person: IPerson): void {
console.log(`Hello ${person.name}`);
}

const me = { name: 'Lee', age: 18 };
sayHello(me); // He

변수 me는 인터페이스 IPerson과 일치하지는 않는다. 하지만 IPerson의 name 프로퍼티를 가지고 있으면 인터페이스에 부합하는 것으로 인정된다.

```

### 선택적 프로퍼티
- 인터페이스의 프로퍼티는 반드시 구현되어야 한다. 하지만 인터페이스의 프로퍼티가 선택적으로 필요한 경우가 있을 수 있다. 선택적 프로퍼티(Optional Property)는 프로퍼티명 뒤에 ?를 붙이며 생략하여도 에러가 발생하지 않는다.

```

interface UserInfo {
username: string;
password: string;
age? : number;
address?: string;
}

const userInfo: UserInfo = {
username: 'ungmo2@gmail.com',
password: '123456'
}

console.log(userInfo);

```



## 제네릭 (Generic)
- 제네릭은 선언 시점이 아니라 생성 시점에 타입을 명시하여 하나의 타입만이 아닌 다양한 타입을 사용할 수 있도록 하는 기법이다. 한 번의 선언으로 다양한 타입에 재사용이 가능하다는 장점이 있다.

T는 제네릭을 선언할 때 관용적으로 사용되는 식별자로 타입 파라미터(Type parameter)라 한다. T는 Type의 약자로 반드시 T를 사용하여야 하는 것은 아니다.

또한 함수에도 제네릭을 사용할 수 있다. 제네릭을 사용하면 하나의 타입만이 아닌 다양한 타입의 매개변수와 리턴값을 사용할 수 있다


```

function reverse<T>(items: T[]): T[] {
return items.reverse();
}

const arg = [1, 2, 3, 4, 5];
// 인수에 의해 타입 매개변수가 결정된다.
const reversed = reverse(arg);
console.log(reversed); // [ 5, 4, 3, 2, 1 ]

function reverse<T>(items: T[]): T[] {
return items.reverse();
}

const arg = [{ name: 'Lee' }, { name: 'Kim' }];
// 인수에 의해 타입 매개변수가 결정된다.
const reversed = reverse(arg);
console.log(reversed); // [ { name: 'Kim' }, { name: 'Lee' } ]

```

```
