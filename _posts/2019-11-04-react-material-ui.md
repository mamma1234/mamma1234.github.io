---
layout: post
title: "React-Material-UI"
description: 
headline: 
modified: 2019-11-14
category: webdevelopment
imagefeature: cover3.jpg
tags: [React, Next, Material]
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

## 설치
### React.js
- npx create-react-app react-material-ui
- cd react-material-ui
- npm install @material-ui/core
- npm install contentful
- npm start
- http://localhost:3000/
- npm install @material-ui/icons

### Next.js
- npm init
- npm install --save react react-dom next@7.0.2 express
- npm install --save-dev @babel/node @babel/preset-env
- npm install --save @material-ui/core @material-ui/icons @material-ui/styles

```
next // 내장되어 있는 webpack-dev-server로 기동
next build // 프로젝트를 빌드하여 .next 폴더를 생성한다.
next start // 빌드된 .next 폴더를 기준으로 웹 서버를 기동해준다.
next export // html 파일들로 내보내기를 해준다.
```

#### Next.js 기본 구조
```
pages/ // HTML Document, Application Container, 각종 페이지 등을 작성한다.
    _document.js // HTML Document.
    _app.js // Application Container. 공통의 레이아웃을 작성한다.
    _error.js // Error Page.
    index.js // Root Page /로 시작되는 경로를 말한다.
    hello.js // Hello Page /hello로 시작되는 경로를 말한다.
static/ // 정적 파일 (이미지, 파일 등)을 업로드 한다.
next.config.js // Next.js의 환경 설정 파일이다. 라우팅 설정, typescript, less 등의 webpack 플러그인을 설정한다.

_document.js    SPA에서 시작점이 되는 index.html이라고 생각하면 된다.
_app.js         React에서 대부분 App.js이라는 이름으로 공통의 레이아웃을 작성하듯이 Next.js에서는 Application의 공통 레이아웃을 _app.js에서 작성할 수 있다.
_error.js       Error 처리를 공통으로 하고자 할 때, 공통적으로 사용할 수 있는 Error Page를 작성할 수 있다.
next.config.js  webpack plugin들과 Next.js의 라우팅 설정을 작성한다.
```