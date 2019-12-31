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
```