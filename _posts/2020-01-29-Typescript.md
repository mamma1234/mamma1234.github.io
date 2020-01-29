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

## compileOptiosn: module

## Type assertions

## 타입 별칭 (별명)