---
layout: post
title: "React Webpack"
description: 
headline: 
modified: 2021-04-30
category: webdevelopment
imagefeature: cover3.jpg
tags: [React Webpack]
mathjax: 
chart: 
share: true
comments: true
featured: true
disqus:
---

# Record
## React 개발 환경을 구축하면서 배우는 웹팩(Webpack) 기초

### 프로젝트 설정하기
- webpack-react 디렉터리 생성
- yarn init -y
- yarn add -D @babel/core @babel/preset-env @babel/preset-react babel-loader clean-webpack-plugin css-loader html-loader html-webpack-plugin mini-css-extract-plugin node-sass react react-dom sass-loader style-loader webpack webpack-cli webpack-dev-server

### 웹팩으로 자바스크립트 파일 빌드하기
- src 디렉터리를 만드신 후 아래와 같이 test.js 파일을 작성
```JavaScript
console.log("webpack test");
```