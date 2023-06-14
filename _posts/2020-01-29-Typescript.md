---
layout: post
title: 'Typescript'
description:
headline:
modified: 2020-01-29
category: Laguage
imagefeature:
tags: [Typescript]
mathjax:
chart:
share: true
comments: true
featured: true
disqus:
---

# Typescript

## Introduction

-   TypeScript는 컴파일하면 JavaScript가 되는(compile-to-JavaScript) 언어이며, 컴파일 시점에 타입 체크를 하고, 전통적인 객체기반 프로그래밍 패턴을 도입하는 것 이외에도 강력한 기능들을 JavaScript 에 추가한다.
-   "JavaScript는 특이한 점이 좀 있는데, 컴파일러에게 이런 것들을 알려주고 전부 체크하기만 하면 된다." - Anders Hejlsberg

## 장점

### 정적타입

-   TypeScript를 사용하는 가장 큰 이유 중 하나는 정적 타입을 지원한다는 것

```
    function sum(a: number, b: number) {
    return a + b;
    }

    sum('x', 'y');
    // error TS2345: Argument of type '"x"' is not assignable to parameter of type 'number'.
```

### 도구의 지원

### 강력한 객체지향 프로그래밍 지원

-   인터페이스, 제네릭 등과 같은 강력한 객체지향 프로그래밍 지원은 크고 복잡한 프로젝트의 코드 기반을 쉽게 구성할 수 있도록 도우며, Java, C# 등의 클래스 기반 객체지향 언어에 익숙한 개발자가 자바스크립트 프로젝트를 수행하는 데 진입 장벽을 낮추는 효과도 있다.

### ES6 / ES Next 지원

### Angular

## 설치

```JavaScript
    $ npm install -g typescript
    $ tsc -v
    Version 2.8.3

    yarn global add typescript
```

## 기초 사용

-   TypeScript 컴파일러(tsc)는 TypeScript 파일(.ts)을 자바스크립트 파일로 트랜스파일링한다.
    이때 트랜스파일링된 person.js의 자바스크립트 버전은 ES3이다. 이는 TypeScript 컴파일 타겟 자바스크립트 기본 버전이 ES3이기 때문이다.

```JavaScript
    // person.ts
    class Person {
        private name: string;

        constructor(name: string) {
            this.name = name;
        }

        sayHello() {
            return "Hello, " + this.name;
        }
    }

    const person = new Person('Lee');

    console.log(person.sayHello());


    $ tsc person

    // person.js - ES3
    var Person = /** @class */ (function () {
        function Person(name) {
            this.name = name;
        }
        Person.prototype.sayHello = function () {
            return "Hello, " + this.name;
        };
        return Person;
    }());
    var person = new Person('Lee');
    console.log(person.sayHello());
```

-   만약, 자바스크립트 버전을 변경하려면 컴파일 옵션에 --target 또는 -t를 사용한다. 현재 tsc가 지원하는 자바스크립트 버전은 ‘ES3’(default), ‘ES5’, ‘ES2015’, ‘ES2016’, ‘ES2017’, ‘ES2018’, ‘ES2019’, ‘ESNEXT’이다. 예를 들어, ES6 버전으로 트랜스파일링을 실행하려면 아래와 같이 옵션을 추가한다.

```JavaScript
    $ tsc person -t ES2015

    // person.js
    class Person {
        constructor(name) {
            this.name = name;
        }
        sayHello() {
            return "Hello, " + this.name;
        }
    }
    const person = new Person('Lee');
    console.log(person.sayHello());
```

## tsconfig

-   매번 옵션을 지정하는 것은 번거로우므로 tsc 옵션 설정 파일을 생성하도록 하자.
    tsc 명령어 뒤에 파일명을 지정하면 tsconfig.json이 무시되므로 주의하기 바란다.

```JavaScript
    $ tsc --init
    message TS6071: Successfully created a tsconfig.json file.

    {
    "compilerOptions": {
        /* Basic Options */
        // "incremental": true,                   /* Enable incremental compilation */
        "target": "es5",                          /* Specify ECMAScript target version: 'ES3' (default), 'ES5', 'ES2015', 'ES2016', 'ES2017', 'ES2018', 'ES2019' or 'ESNEXT'. */
        "module": "commonjs",                     /* Specify module code generation: 'none', 'commonjs', 'amd', 'system', 'umd', 'es2015', or 'ESNext'. */
        // "lib": [],

    $ tsc person //tsconfig.json이 무시된다.

    $ tsc //파일명을 지정하지 않으면 프로젝트 폴더 내의 모든 TypeScript 파일이 모두 트랜스파일링된
```

```JavaScript
    --watch 또는 -w 옵션을 사용하면 트랜스파일링 대상 파일의 내용이 변경되었을 때 이를 감지하여 자동으로 트랜스파일링이 실행된다.
    $ tsc --watch
    21:23:30 - Compilation complete. Watching for file changes.

    //tsconfig.json에 watch 옵션을 추가
    {
        // ...
        "watch": true
    }

    [오전 12:40:06] File change detected. Starting incremental compilation...

    [오전 12:40:07] Found 0 errors. Watching for file changes.


    yarn add tsc-watch --dev
    이후 바로 yarn add typescript를 해준다
    tsc-watch가 global패키지를 읽지 못하는 듯하다. 그래서 새로 설치한다.
```

## Typescript Compile Option을 설정할 수 있다.

-   files > exlucde > include

## @types

## compileOptions: target, lib

-   target
    -   ts file을 js file로 compile할 때 어떤 버전의 js 스펙을 적용할 지 ex) es3, es5
    -   default: es3
-   lib
    -   기본 type definition 라이브러리를 어떤 것을 사용할 지
    -   lib 지정안할 경우,
        -   target = es3, default로 lib.d.ts
        -   target = es5, default로 dom,es5,scripthost
        -   target = es6, default로 dom,es6,dom.iterable,scripthost
    -   lib를 지정하면 그 lib 배열로만 라이브러리를 사용한다.
        -   빈 [] => 'no definition found 샬라샬라'

## compileOptions: outDir, outFile

-   outFile -> 하나의 file로 type을 만들 경우
-   outDir -> 디렉토리 그대로 type 만들 경우

## compileOptiosn: module

-   컴파일 된 모듈의 결과물을 어떤 모듈 시스템으로 할지 결정 module ex) commonJS, systemJS 등등
-   target = es6 -> es6가 디폴트 / 아닐 경우 commonJS가 디폴트
-   moduleResoliution -> ts 소스에서 모듈을 사용하는 방식 지정. Classic 아니면 Node 이다.
-   paths 와 baseUrl은 가져올때 사용하는 것, 상대경로 방식이 아닌 baseUrl로 꼭지점과 paths 안의 키/밸류로 모듈을 가져가는 방식.
-   rootDirs: 배열 안에서 상대 경로를 찾는 방식. -> 모듈 가져올 떄 모듈 path에 대한 root지정.

## Type assertions

-   형변환과는 다르다. -> 실제 데이터 구조를 바꾸지 않음.
-   컴파일러에게 'Type이 이것이다' 라고 알려주는 것을 의미한다.
-   문법적으로는 2가지 방법이 있다.
    -   변수 as 강제할타입
    -   <강제할타입>변수

## 타입 별칭 (별명)

-   Primitve, Union Type, Tuple
-   Interface와 비슷하다.
-   기타 직접 작성해야하는 타입을 다른 이름으로 지정할 수 있따.
-   만들어진 타입의 refer 로 사용하는 것이지 타입을 새로 만드는것이 아니다.
-   \*\*Interface 와의 차이점
    -   Type Alias는 실제 Type이 새로 정의된 것이 아닌 해당 Type에 대한 refer인 반면, Interface는 새로 정의한 Type이다.
    -   Type Alias는 Type Alias끼리 상속 불가능.

## 문법

### 타입 표기 (Type Annotation)

-   value: type 의 형태로 표기

```JavaScript
    const areYouCool: boolean = true;
    const hasType: Object = {
    TypeScript: true,
    JavaScript: false
    };
```

### 기본 타입

-   boolean, number, string, null, undefined, any, void (null, undefined), never

```JavaScript
    let bool: any = true;
    bool = 3;
    bool = 'whatever';
    bool = {};

    function alwaysThrow(): never {
    throw new Error(`I'm a wicked function!`);
    }
```

### 배열과 튜플

```JavaScript
    const pibonacci: number[] = [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55];
    const myFavoriteBeers: string[] = ['Imperial Stout', 'India Pale Ale', 'Weizenbock'];
    const pibonacci: Array<number> = [0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55];
    const myFavoriteBeers: Array<string> = ['Imperial Stout', 'India Pale Ale', 'Weizenbock'];
```

```JavaScript
    const nameAndHeight: [string, number] = ['안희종', 176]
    nameAndHeight.push(42); // no error
```

### 객체

-   자바스크립트의 오브젝트 리터럴을 정의하듯 중괄호({})를 이용해 객체 타입(object type)을 표현할 수 있다.

```JavaScript
    const user: { name: string; height: number; } = { name: '안희종', height: 176 };
```

-   구분자로 콤마(,) 뿐만 아니라 세미콜론(;)을 사용할 수 있다.
-   물음표(?)를 붙여 해당 속성이 존재하지 않을 수도 있음을 표현

```JavaScript
    const userWithUnknownHeight: { name: string; height?: number; } = {
    name: '김수한무'
    };
```

-   readonly 키워드를 붙여 해당 속성의 재할당을 막을 수 있다. readonly 키워드가 붙은 속성은 const 키워드를 이용한 변수의 정의와 비슷하게 동작한다.

```JavaScript
    const user: {
    readonly name: string;
    height: numer;
    } = { name: '안희종', height: 176 };
    user.name = '종희안'; // error TS2540: Cannot assign to 'name' because it is a constant or a read-only property.
```

### 타입 별칭

-   타입 별칭(type alias)을 이용해 이미 존재하는 타입에 다른 이름을 붙여 복잡한 타입을 간단하게 쓸 수 있다

```JavaScript
    type NewType = Type;
    type UUID = string;
    type Height = number;
    type AnotherUUID = UUID;
    type Animals = Animal[];
    type User = {
    name: string;
    height: number;
    };
```

### 함수

```JavaScript
    function sum(a: number, b: number): number {
        return (a + b);
    }

    function logGreetings(name: string): void {
        console.log(`Hello, ${name}!`);
    }

    function greetings(name: string = 'stranger'): void {
        console.log(`Hello, ${name}`);
    }

    function fetchVideo(url: string, subtitleLanguage?: string) {
        const option = { url };
        if (subtitleLanguage) {
            option.subtitleLanguage = true;
        }
    /* ... */
    }

    const yetAnotherSum: (a: number, b: number) => number = sum;

    const onePlusOne: () => number = () => 2;

    const arrowSum: (a: number, b: number) => number = (a, b) => (a + b);

    type SumFunction = (a: number, b: number) => number;
    const definitelySum: SumFunction = (a, b) => (a + b);
```

-   함수 오버로딩
    -   함수는 하나 이상의 타입 시그니처를 가질 수 있다.
    -   함수는 단 하나의 구현을 가질 수 있다.

```JavaScript
    function double(str: string): string;
    function double(num: number): number;
    function double(arr: boolean[]): boolean[];

    function double(arg) {
        if (typeof arg === 'string') {
            return `${arg}${arg}`;
        } else if (typeof arg === 'number') {
            return arg * 2;
        } else if (Array.isArray(arg)) {
            return arg.concat(arg);
        }
    }

    const num = double(3); // number
    const str = double('ab'); // string
    const arr = double([true, false]); // boolean[]
```

-   This 타입

```JavaScript
    interface HTMLElement {
        tagName: string;
    /* ... */
    }
    interface Handler {
        (this: HTMLElement, event: Event, callback: () => void): void;
    }
    let cb: any;
    // 실제 함수 매개변수에는 this가 나타나지 않음
    const onClick: Handler = function(event, cb) {
        // this는 HTMLElement 타입
        console.log(this.tagName);
        cb();
    }

    //this의 타입을 void로 명시한다면 함수 내부에서 this에 접근하는 일 자체를 막을 수 있다
    interface NoThis {
        (this: void): void;
    }
    const noThis: NoThis = function() {
        console.log(this.a); // Property 'a' does not exist on type 'void'.
    }
```

### 제너릭

-   제너릭을 이용해 여러 타입에 대해 동일한 규칙을 갖고 동작하는 타입을 정의할 수 있다.

```JavaScript
    function getFirstElem(arr: string[]): string;
    function getFirstElem(arr: number[]): number;
    function getFirstElem(arr) {
    if (!Array.isArray(arr)) {
        throw new Error('getFirstElemOrNull: Argument is not array!');
    }
    if (arr.length === 0) {
        throw new Error('getFirstElemOrNull: Argument is an empty array!');
    }
    return arr[0] ? arr[0] : null;
    }
```

-   타입 변수 <T>

```JavaScript
    //타입변수 활용 제너릭 함수
    function getFirstElem<T>(arr: T[]): T {
    /* 함수 본문 */
    }
```

-   여러 타입에 대해 동작하는 요소를 정의하되, 해당 요소를 사용할 때가 되어야 알 수 있는 타입 정보를 정의에 사용하는 것

### 유니온 타입

-   유니온 타입을 이용해 “여러 경우 중 하나”인 타입을 표현할 수 있다.

```JavaScript
    function square(value: number, returnString: boolean): number;
    function square(value: number, returnString: boolean): string;
    function square(value, returnString = false) {
    /* 본문 동일 */
    }
    const mystery: ??? = square(randomNumber, randomBoolean);

    function square(value: number, returnString: boolean = false): string | number {
    /* 본문 동일 */
    }
    const stringOrNumber: string | number = square(randomNumber, randomBoolean);

    type SquaredType = string | number;
    function square(value: number, returnOnString: boolean = false): SquaredType {
    /* 본문 동일 */
    }

    type Fruits =
        | Apple
        | Banana
        | Cherry;
```

### 인터섹션 타입

-   인터섹션 타입을 이용해 “여러 경우에 모두 해당”하는 타입을 표현할 수 있다.

```JavaScript
    type Programmer = { favoriteLanguage: string };
    const programmer: Programmer = { favoriteLanguage: 'TypeScript' };

    type BeerLover = { favoriteBeer: string };
    const beerLover: BeerLover = { favoriteBeer: 'Imperial Stout' };

    type BeerLovingProgrammer = Programmar & BeerLover;

    type BeerLovingProgrammer2 =
        & Programmer
        & BeerLover;
```

### 열거형

-   유한한 경우의 수를 갖는 값의 집합을 표현하기 위해 사용하는 열거형(enum) 타입

-   숫자 열거형은 number 타입 값에 기반한 열거형이다. 만약 열거형을 정의하며 멤버의 값을 초기화하지 않을 경우, 해당 멤버의 값은 0부터 순차적으로 증가하는 숫자 값을 갖는다

@ 는 this 를 대신한다. 그러므로 this.user 는 @user 이다.

## interface

-   인터페이스(interface)를 통해 값이 따라야 할 제약을 타입으로 표현 할 수 있다. 인터페이스 타입을 통해 값의 형태(shape)를, 즉 값이 어떤 멤버를 가져야 하고 각 멤버의 타입은 어때야 하는지를 서술할 수 있다.

```JavaScript
    interface User {
        name: string;
        height: number;
    }

    interface User {
        name: string;
        readonly height: number;
        favoriteLanguage?: string;
    }
    const author: User = { name: '안희종', height: 176 }; // ok
    author.height = 183; // error TS2540: Cannot assign to 'height' because it is a constant or a read-only property.
```

-   함수 인터페이스
    -   (매개변수1 이름: 매개변수1 타입, 매개변수2 이름: 매개변수2 타입, ...): 반환 타입

```JavaScript
    interface GetUserName {
        (user: User): string;
    }
    const getUserName: GetUserName = function (user) {
        return user.name;
    };
```

-   하이브리드 타입

```JavaScript
    interface Counter {
        (start: number): string;
        interval: number;
        reset(): void;
    }
    function getCounter(): Counter {
        let counter = <Counter>function (start: number) { };
        counter.interval = 123;
        counter.reset = function () { };
        return counter;
    }
    let c = getCounter();
    c(10);
    c.reset();
    c.interval = 5.0;
```

-   제너릭 인터페이스

```JavaScript
    interface MyResponse<Data> {
        data: Data;
        status: number;
        ok: boolean;
        /* ... */
    }
    inteface User {
        name: string;
        readonly height: number;
        /* ... */
    }
    const user: MyReponse<User> = await getUserApiCall(userId);
    user.name; // 타입 시스템은 user.name이 string임을 알 수 있다.


    interface GetData {
       <Data>(response: MyResponse<Data>): Data;
    }
```

### 색인 가능 타입

-   동적인 색인을 표현하는 색인 가능 타입

-   색인 시그니쳐

```JavaScript
    interface NameHeightMap {
    [userName: string]: number | undefined;
    }
```

### 인터페이스 확장

```JavaScript
    interface LoggedInUser extends User {
    loggedInAt: Date;
    }
```

## class

-   클래스(class)를 이용해 객체 지향 프로그래밍 언어와 비슷한 방식으로 코드를 구조화 할 수 있다. 타입스크립트의 클래스는 ES6에 추가된 클래스 문법의 확장으로, 접근 제어자 등의 유용한 추가 기능을 제공한다.

```JavaScript
    class BarkingDog {
        constructor(barkingSound: string) {
            console.log(`${barkingSound}!`);
        }
    }

    const barkingDog: BarkingDog = new BarkingDog('월'); // 월!


    class BarkingDog {
    barkingSound: string;

    constructor(barkingSound: string) {
        this.barkingSound = barkingSound;
    }

    bark(): void {
        console.log(`${this.barkingSound}!`);
    }
    }
    const barkingDog: BarkingDog = new BarkingDog('월');
    barkingDog.bark(); // 월!
```

### 클래스 확장

```JavaScript
    class Base {
    baseProp: number;
    constructor() {
        this.baseProp = 123;
    }
    }
    class Extended extends Base {
    extendedProp: number;
    constructor() {
        super(); // 반드시 이 호출을 직접 해 주어야 한.
        this.extendedProp = 456;
    }
    }
    const extended: Extended = new Extended();
    console.log(extended.baseProp); // 123
    console.log(extended.extendedProp); // 45
```

### static 스태틱 멤버

```JavaScript
    class Counter {
        static count: number = 0;
        static increaseCount() {
            Counter.count += 1;
        }
        static getCount() {
            return Counter.count;
        }
        }
    console.log(Counter.count); // 0
    Counter.increaseCount();
    console.log(Counter.getCount()); // 1
    Counter.increaseCount();
    console.log(Counter.getCount()); // 2
```

### 접근 제어자

-   public
    -   접근 제한이 전혀 존재하지 않으며, 프로그램의 어느 곳에서나 접근 가능

```JavaScript
    // implicit public member
    class Triangle {
        vertices: number;

        constructor() {
            this.vertices = 3;
        }
    }

    // explicit public member
    class Triangle {
        public vertices: number;

        public constructor() {
            this.vertices = 3;
        }
    }
```

-   private
    -   해당 클래스 내부의 코드만이 접근 가능

```JavaScript
    class User {
        private password: string;

        constructor (password: string) {
            this.password = password;
        }
    }

    const yoonha = new User('486');
    console.log(yoonha.password);
    // error TS2341: Property 'password' is private and only accessible within class 'User'.
```

-   protected
    -   protected 권한의 멤버는 private과 비슷하게 동작하지만, 서브클래스에서의 접근 또한 허용된다는 점이 다르다.

```JavaScript
    class User {
        protected password: string;

        constructor (password: string) {
            this.password = password;
        }
    }

    class CarOwner extends User {
        carId: string;

        constructor (password: string, carId: string) {
            super(password);
            this.carId = carId;
        }

        setPassword(newPassword: string) {
            this.password = newPassword; // Okay
        }
    }
```

-   생성자에서의 접근 제어자

```JavaScript
    class User {
        constructor (public id: string, private password: string) { }
    }

    //동일한 코드

    class User {
        public id: string;
        private password: string;

        constructor (id: string, password: string) {
            this.id = id;
            this.password = password;
        }
    }
```

### 접근자

```JavaScript
    class Shape {
        private _vertices: number = 3;

        getVertices() {
            console.log('Vertices getter called.');
            return this._vertices;
        }

        setVertices(value) {
            console.log('Vertices setter called.');
            this._vertices = value;
        }
    }
```

-   읽기 접근을 위한 게터

```JavaScript
    class Shape {
    constructor (public vertices: number) { }
        get vertices(): number {
            console.log('Vertices getter called.');
            return 3;
        }
    }
    const triangle: Shape = new Shape(3);
    const vertices = triangle.vertices; // Vertices getter called.
    console.log(vertices); // 3
```

-   쓰기 접근을 위한 세터

```JavaScript
    class Shape {
        private _vertices: number = 3;
        get vertices() {
            console.log('Vertices getter called.');
            return this._vertices;
        }
        set vertices(value) {
            console.log('Vertices setter called.');
            this._vertices = value;
        }
    }
    const square = new Shape();
    square.vertices = 4; // Vertices setter called.
    const vertices = square.vertices; // Vertices getter called.
    console.log(vertices); // 4
```

### 추상 클랙스

-   추상 클래스는 인스턴스화가 불가능하다는 점에서 일반 클래스와 다르다
-   추상 클래스는 구현을 일부 포함할 수 있다는 점에서 인터페이스와 다르다.

```JavaScript
    abstract class Animal {
        move(): void {
            console.log("roaming the earth...");
        }
        abstract makeSound(): void;
    }
```

-   가상 클래스를 확장하는 서브 클래스는 슈퍼 클래스의 모든 가상 메소드를 구현해야 한다.

```JavaScript
    class Dog extends Animal { }
    // error TS2515: Non-abstract class 'Dog' does not implement inherited abstract member 'makeSound' from class 'Animal'.
```

## 인터페이스와 클래스의 관계

```JavaScript
    interface Animal {
        legs: number;
    }

    class Dog implements Animal {
        legs: number = 4;
    }
    // Okay

    class Point {
        x: number;
        y: number;
    }

    interface Point3d extends Point {
        z: number;
    }

    const point3d: Point3d = {x: 1, y: 2, z: 3};
```
