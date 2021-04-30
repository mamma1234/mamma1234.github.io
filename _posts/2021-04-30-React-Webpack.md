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

- 최상위 디렉터리로 이동한 후 아래와 같이 webpack.config.js
```JavaScript
  const path = require("path");

  module.exports = {
    entry: "./src/test.js",
    output: {
      filename: "bundle.js",
      path: path.resolve(__dirname + "/build")
    },
    mode: "none"
  };


여기서 entry는 웹팩이 빌드할 파일을 알려주는 역할을 합니다.
이렇게 한다면 src/test.js 파일 기준으로 import 되어 있는 모든 파일들을 찾아 하나의 파일로 합치게 됩니다.

output은 웹팩에서 빌드를 완료하면 output에 명시되어 있는 정보를 통해 빌드 파일을 생성합니다.

mode는 웹팩 빌드 옵션 입니다. production은 최적화되어 빌드되어지는 특징을 가지고 있고 development는 빠르게 빌드하는 특징, none 같은 경우는 아무 기능 없이 웹팩으로 빌드합니다.

```

-  package.json 파일로 이동하신 후 다음과 같이 build: webpack 스크립트를 추가
```JavaScript
{
  "name": "webpack-react",
  "version": "1.0.0",
  "main": "index.js",
  "license": "MIT",
  "scripts": {
    "build": "webpack"
  },
  "devDependencies": {
    "@babel/core": "^7.4.3",
    "@babel/preset-env": "^7.4.3",
    "@babel/preset-react": "^7.0.0",
    "babel-loader": "^8.0.5",
    "clean-webpack-plugin": "^2.0.1",
    "css-loader": "^2.1.1",
    "html-loader": "^0.5.5",
    "html-webpack-plugin": "^3.2.0",
    "mini-css-extract-plugin": "^0.6.0",
    "node-sass": "^4.11.0",
    "react": "^16.8.6",
    "react-dom": "^16.8.6",
    "sass-loader": "^7.1.0",
    "style-loader": "^0.23.1",
    "webpack": "^4.30.0",
    "webpack-cli": "^3.3.1",
    "webpack-dev-server": "^3.3.1"
  }
}

webpack 명령어가 실행되면 디폴트로 실행할 파일은 같은 경로에 있는 webpack.config.js에 내용을 가지고 빌드 됩니다.

yarn build 

그 후 빌드 디렉터리로 이동하면 bundle.js 파일을 볼 수 있습니다.
```

### 웹팩으로 HTML 파일 빌드하기
- 이번에는 html 파일들을 웹팩으로 빌드해 보도록 하겠습니다.
웹팩은 자바스크립트 파일뿐만 아니라 자바스크립트가 아닌 파일들도 모듈로 관리 할 수 있습니다.
로더(loader) 라는 기능이 있습니다. 로더는 자바스크립트 파일이 아닌 파일을 웹팩이 이해할 수 있게 해줍니다.

- public 디렉터리를 만들어 주신 후 public 디렉터리에 다음과 같이 index.html 파일 생성
```JavaScript
<!DOCTYPE html>
<html lang="kr">
  <head>
    <meta charset="utf-8" />
    <title>WEBPACK4-REACT</title>
  </head>
  <body>
    <noscript>스크립트가 작동되지 않습니다!</noscript>
    <div id="root"></div>
  </body>
</html>
```

- webpack.config.js 파일에 아래와 같이 html 관련 코드를 추가
```JavaScript
const path = require("path");
const HtmlWebPackPlugin = require("html-webpack-plugin");

module.exports = {
  entry: "./src/test.js",
  output: {
    filename: "bundle.js",
    path: path.resolve(__dirname + "/build")
  },
  mode: "none",
  module: {
    rules: [
      {
        test: /\.html$/,
        use: [
          {
            loader: "html-loader",
            options: { minimize: true }
          }
        ]
      }
    ]
  },
  plugins: [
    new HtmlWebPackPlugin({
			template: './public/index.html', // public/index.html 파일을 읽는다.
      filename: 'index.html' // output으로 출력할 파일은 index.html 이다.
    })
  ]
};
```