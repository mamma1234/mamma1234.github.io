---
layout: post
title: "Typescript"
description: 
headline: 
modified: 2020-01-29
category: webdevelopment
imagefeature: cover3.jpg
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


## 장점
### 정적타입
- TypeScript를 사용하는 가장 큰 이유 중 하나는 정적 타입을 지원한다는 것
```
    function sum(a: number, b: number) {
    return a + b;
    }

    sum('x', 'y');
    // error TS2345: Argument of type '"x"' is not assignable to parameter of type 'number'.
```

### 도구의 지원
### 강력한 객체지향 프로그래밍 지원
- 인터페이스, 제네릭 등과 같은 강력한 객체지향 프로그래밍 지원은 크고 복잡한 프로젝트의 코드 기반을 쉽게 구성할 수 있도록 도우며, Java, C# 등의 클래스 기반 객체지향 언어에 익숙한 개발자가 자바스크립트 프로젝트를 수행하는 데 진입 장벽을 낮추는 효과도 있다.
### ES6 / ES Next 지원
### Angular

## 설치
```
    $ npm install -g typescript
    $ tsc -v
    Version 2.8.3
```
- TypeScript 컴파일러(tsc)는 TypeScript 파일(.ts)을 자바스크립트 파일로 트랜스파일링한다.


## Traditional Compiled Langauge


## tsconfig
Typescript Compile Option을 설정할 수 있다.
- files > exlucde > include

## @types

## compileOptions: target, lib
- target
    - ts file을 js file로 compile할 때 어떤 버전의 js 스펙을 적용할 지 ex) es3, es5
    - default: es3
- lib
    - 기본 type definition 라이브러리를 어떤 것을 사용할 지
    - lib 지정안할 경우,
        - target = es3, default로 lib.d.ts
        - target = es5, default로 dom,es5,scripthost
        - target = es6, default로 dom,es6,dom.iterable,scripthost
    - lib를 지정하면 그 lib 배열로만 라이브러리를 사용한다.
        - 빈 [] => 'no definition found 샬라샬라'

## compileOptions: outDir, outFile
- outFile -> 하나의 file로 type을 만들 경우
- outDir -> 디렉토리 그대로 type 만들 경우

## compileOptiosn: module
- 컴파일 된 모듈의 결과물을 어떤 모듈 시스템으로 할지 결정 module ex) commonJS, systemJS 등등
- target = es6 -> es6가 디폴트 / 아닐 경우 commonJS가 디폴트
- moduleResoliution -> ts 소스에서 모듈을 사용하는 방식 지정. Classic 아니면 Node 이다.
- paths 와 baseUrl은 가져올때 사용하는 것, 상대경로 방식이 아닌 baseUrl로 꼭지점과 paths 안의 키/밸류로 모듈을 가져가는 방식.
- rootDirs: 배열 안에서 상대 경로를 찾는 방식. -> 모듈 가져올 떄 모듈 path에 대한 root지정.

## Type assertions
- 형변환과는 다르다. -> 실제 데이터 구조를 바꾸지 않음.
- 컴파일러에게 'Type이 이것이다' 라고 알려주는 것을 의미한다.
- 문법적으로는 2가지 방법이 있다.
    - 변수 as 강제할타입
    - <강제할타입>변수

## 타입 별칭 (별명)
- Primitve, Union Type, Tuple
- Interface와 비슷하다.
- 기타 직접 작성해야하는 타입을 다른 이름으로 지정할 수 있따.
- 만들어진 타입의 refer 로 사용하는 것이지 타입을 새로 만드는것이 아니다.
- **Interface 와의 차이점
    - Type Alias는 실제 Type이 새로 정의된 것이 아닌 해당 Type에 대한 refer인 반면, Interface는 새로 정의한 Type이다.
    - Type Alias는 Type Alias끼리 상속 불가능.