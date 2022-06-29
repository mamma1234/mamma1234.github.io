---
layout: post
title: 'Webpack'
description:
headline:
modified: 2019-10-08
category: webdevelopment
imagefeature:
tags: [Webpack]
mathjax:
chart:
share: true
comments: true
featured: true
disqus:
---

# Webpack

## 개념

모던 자바스크립트 어플리케이션을 위한 스태틱 모듈 번들러
(static module bundler for modern JavaScript applications)
프로젝트에서 필요한 모든 모듈을 의존성 그래프를 만들어 매핑 -> 하나, 혹은 그 이상의 번들 생성

## 핵심 개념

### 엔트리 Entry

-   의존성 그래프의 시작점을 웹팩에서는 엔트리(entry)라고 한다.

```
module.exports = {
  entry: {
    main: './src/main.js',
  }
}
```

### 아웃풋 Output

-   엔트리에 설정한 자바스크립트 파일을 시작으로 의존되어 있는 모든 모듈을 하나로 묶을 것이다. 번들된 결과물을 처리할 위치는 output에 기록한다.

```
module.exports = {
  output: {
    filename: 'bundle.js',
    path: './dist'
  }
}

<body>
  <script src="./dist/bundle.js"></script>
</body>
```

### 로더 Loaders

-   자바스크립트 파일 뿐만 아니라 이미지, 폰트, 스타일시트도 전부 모듈로 관리한다. 그러나 웹팩은 자바스크립트 밖에 모른다. 비 자바스크립트 파일을 웹팩이 이해하게끔 변경해야하는데 로더가 그런 역할을 한다

```
test에 로딩할 파일을 지정하고
use에 적용할 로더를 설정한다

ES6 -> ES5
module.exports = {
  module: {
    rules: [{
      test: /\.js$/,
      exclude: 'node_modules',
      use: {
        loader: 'babel-loader',
        options: {
          presets: ['env']
        }
      }
    }]
  }
}
```

### 플러그인 Plugins

-   UglifyJsPlugin

```
자바스크립트 결과물을 난독화 처리
module.exports = {
  plugins: [
    new webpack.optimize.UglifyJsPlugin(),
  ]
}

```

-   ExtractTextPlugin

```
텍스트 추출
module.exports = {
  module: {
    rules: [{
      test: /\.scss$/,
      use: ['style-loader', 'css-loader', 'sass-loader']
    }]
  }
};

```

## 주요 CLI 및 기능

-   npm i -g webpack-cli
-   webpack app/index.js --output dist/bundle.js --mode development

## webpack.config.js

-   webpack

```
module.exports = {
  module: {
    rules: [{
      test: /\.js$/,
      exclude: 'node_modules',
      use: {
        loader: 'babel-loader',
        options: {
          presets: ['env']
        }
      }
    }]
  }
}

npm i --save-dev babel-loader babel-core babel-preset-env
```

-   css-loader, style-loader

```
module.exports = {
  module: {
    rules: [{
      test: /\.css$/,
      use: ['style-loader', 'css-loader']
    }]
  }
};

```

## bundel.js

-

# Babel

## 개념

Babel은 ECMAScript 2015+ 코드를 이전 JavaScript 엔진에서 실행할 수있는 이전 버전과 호환되는 JavaScript 버전으로 변환하는 데 주로 사용되는 무료 오픈 소스 JavaScript 컴파일러입니다.

Babel
@babel/cli : 7.7.0
@babel/core : 7.7.2
@babel/preset-env : 7.7.1
@babel/plugin-proposal-class-properties : 7.7.0
@babel/polyfill : 7.7.4
