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

html-webpack-plugin은 웹팩이 html 파일을 읽어서 html 파일을 빌드할 수 있게 해줍니다.

위에 있는 로더는 html 파일을 읽었을 때 html-loader를 실행하여 웹팩이 이해할 수 있게 하고 options 으로는 minimize 라는 코드 최적화 옵션을 사용하고 있습니다.

그 후 yarn build 명령어를 실행해 주시면 다음과 같이 build/index.html 파일이 생성되어 있는 모습을 볼 수 있습니다.

minimize 옵션이 켜져 있어서 파일 내용이 한줄로 되어 있습니다. minimize 옵션을 꺼주시면 줄바꿈된 형태로 보여집니다. 또한 HtmlWebpackPlugin은 웹팩 빌드시 output에 있는 bundole.js를 자동으로 import 합니다.

index.html 을 웹브라우저에서 보시면 콘솔창에 webpack test 가 찍히는 것을 볼 수 있습니다.

```


### 웹팩으로 리액트 빌드하기
- src/index.js
```JavaScript
import React from "react";
import ReactDOM from "react-dom";
import Root from "./Root";

ReactDOM.render(<Root />, document.getElementById("root"))
```

- src/Root.js
```JavaScript
import React from 'react';

const Root = () => {
  return (
    <h3>Hello, React</h3>
  );
};

export default Root;
```

- 최상위 디렉터리에서 .babelrc 파일 생성
  - 바벨 (babel)은 ES6에서 ES5로 자바스크립트를 변환해주는 역할을 합니다. 아래 내용은 바벨이 ES6와 리액트를 ES5로 변환할 수 있게 해준다는 내용입니다.
```JavaScript
{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```

- webpack.config.js 파일에 entry와 rules에 babel-loader를 추가
```JavaScript
const path = require("path");
const HtmlWebPackPlugin = require("html-webpack-plugin");

module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "bundle.js",
    path: path.resolve(__dirname + "/build")
  },
  mode: "none",
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: "/node_modules",
        use: ['babel-loader'],
      },
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

- yarn build 명령어를 실행해 웹팩으로 빌드한 후 index.html 파일을 열어보면 Hello, React가 보이는 모습을 확인


### 웹팩에서 CSS 사용하기
- src/style.css 생성
```JavaScript
.title {
	color: #2196f3;
    font-size: 52px;
    text-align: center;
}
```

- src/root.js에서 style.css
```JavaScript
import React from 'react';
import './style.css';

const Root = () => {
  return (
    <h3 className="title">Hello, React</h3>
  );
};

export default Root;
```

- webpack.config.js에 css-loader를 추가
```JavaScript
const path = require("path");
const HtmlWebPackPlugin = require("html-webpack-plugin");

module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "bundle.js",
    path: path.resolve(__dirname + "/build")
  },
  mode: "none",
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: "/node_modules",
        use: ['babel-loader'],
      },
      {
        test: /\.html$/,
        use: [
          {
            loader: "html-loader",
            options: { minimize: true }
          }
        ]
      },
      {
        test: /\.css$/,
        use: ['css-loader']
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

```JavaScript
하지만 build가 완료된 index.html 파일을 웹브라우저에서 열어보면 css가 적용이 안되어 있습니다.

왜냐하면, 웹팩에서 css 파일을 읽은 후 어딘가에 저장을 해야하기 때문입니다.

이럴때, css를 index.html에 합치는 방법도 있지만 파일을 추출해 보도록 하겠습니다!

webpack.config.js에 CSS를 추출해서 파일로 저장하는 플러그인을 적용하겠습니다.


const path = require("path");
const HtmlWebPackPlugin = require("html-webpack-plugin");
const MiniCssExtractPlugin = require("mini-css-extract-plugin");

module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "bundle.js",
    path: path.resolve(__dirname + "/build")
  },
  mode: "none",
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: "/node_modules",
        use: ['babel-loader'],
      },
      {
        test: /\.html$/,
        use: [
          {
            loader: "html-loader",
            options: { minimize: true }
          }
        ]
      },
      {
        test: /\.css$/,
        use: [MiniCssExtractPlugin.loader, 'css-loader']
      }
    ]
  },
  plugins: [
    new HtmlWebPackPlugin({
      template: './public/index.html', // public/index.html 파일을 읽는다.
      filename: 'index.html' // output으로 출력할 파일은 index.html 이다.
    }),
    new MiniCssExtractPlugin({
      filename: 'style.css'
    })
  ]
};
```

```JavaScript
{
test: /\.css$/,
use: [MiniCssExtractPlugin.loader, 'css-loader']
}
use에 있는 loader 순서는 오른쪽에서 왼쪽 순서로 실행이 됩니다.
위에 있는 코드에 의미는 css-loader로 css 파일을 읽고 MniCssExtractPlugin.loader로 읽은 CSS를 파일로 추출해 냅니다.
```


### 웹팩에서 SCSS 사용하기
- src/style.scss 생성
```JavaScript
$fontColor: #2196f3;
$fontSize: 52px;


.title {
  color: $fontColor;
  font-size: $fontSize;
  text-align: center;
}
```

- src/Root.js를 아래와 같이 scss를 import
```JavaScript
import React from 'react';
import './style.scss';

const Root = () => {
  return (
    <h3 className="title">Hello, React</h3>
  );
};

export default Root;
```

- webpack.config.js를 열어 아래와 같이 sass-loader를 적용
```JavaScript
const path = require("path");
const HtmlWebPackPlugin = require("html-webpack-plugin");
const MiniCssExtractPlugin = require("mini-css-extract-plugin");

module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "bundle.js",
    path: path.resolve(__dirname + "/build")
  },
  mode: "none",
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: "/node_modules",
        use: ['babel-loader'],
      },
      {
        test: /\.html$/,
        use: [
          {
            loader: "html-loader",
            options: { minimize: true }
          }
        ]
      },
      {
        test: /\.css$/,
        use: [MiniCssExtractPlugin.loader, 'css-loader']
      },
      {
        test: /\.scss$/,
        use: [MiniCssExtractPlugin.loader, "css-loader", "sass-loader"]
      }
    ]
  },
  plugins: [
    new HtmlWebPackPlugin({
      template: './public/index.html', // public/index.html 파일을 읽는다.
      filename: 'index.html' // output으로 출력할 파일은 index.html 이다.
    }),
    new MiniCssExtractPlugin({
      filename: 'style.css'
    })
  ]
};
```

```JavaScript
use: [MiniCssExtractPlugin.loader, "css-loader", "sass-loader"]
위에 부분을 해석하면 먼저 sass-loader로 scss 파일을 읽고 css로 변환한 후 css-loader로 css 읽습니다. 그 후 MiniCssExtractPlugin으로 읽은 CSS를 파일로 추출합니다.
```


### 웹팩 개발 서버 적용하기

- 지금까지 소스코드를 수정할 때마다 웹팩으로 직접 빌드를 했습니다.
  수정할때 마다 직접 빌드하면 많이 불편할 것 같습니다.

  이런 불편한 점때문에 소스코드를 수정할때마다 알아서 웹팩이 빌드해주는 webpack-dev-server가 있습니다.

  바로 webpack-dev-server를 적용해보도록 하겠습니다.

  먼저, webpack.config.js 파일에 들어가 devServer를 추가해 줍시다.


```JavaScript
const path = require("path");
const HtmlWebPackPlugin = require("html-webpack-plugin");
const MiniCssExtractPlugin = require("mini-css-extract-plugin");

module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "bundle.js",
    path: path.resolve(__dirname + "/build")
  },
  devServer: {
    contentBase: path.resolve("./build"),
    index: "index.html",
    port: 9000
  },
  mode: "none",
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: "/node_modules",
        use: ['babel-loader'],
      },
      {
        test: /\.html$/,
        use: [
          {
            loader: "html-loader",
            options: { minimize: true }
          }
        ]
      },
      {
        test: /\.css$/,
        use: [MiniCssExtractPlugin.loader, 'css-loader']
      },
      {
        test: /\.scss$/,
        use: [MiniCssExtractPlugin.loader, "css-loader", "sass-loader"]
      }
    ]
  },
  plugins: [
    new HtmlWebPackPlugin({
      template: './public/index.html', // public/index.html 파일을 읽는다.
      filename: 'index.html' // output으로 출력할 파일은 index.html 이다.
    }),
    new MiniCssExtractPlugin({
      filename: 'style.css'
    })
  ]
};

그 후 package.json 파일에 들어가 scripts에 다음과 같이 yarn start를 추가해 줍니다.

"scripts": {
	"build": "webpack",
	"start": "webpack-dev-server --hot"
}
그런다음 터미널에서 yarn start를 실행해주세요

```

### 빌드 디렉터리 깨끗하게 하기

```JavaScript
이번에는 build 디렉터리를 clean-webpack-plugin 을 통해서 빌드될때마다 안쓰는 파일들을 삭제할 수 있게 하겠습니다.

먼저, webpack.config.js에서 아래와 같이 plugins에 MiniCssExtractPlugin에 filename을 style-test.css로 변경해 주세요


plugins: [
	new HtmlWebPackPlugin({
		template: './public/index.html', // public/index.html 파일을 읽는다.
		filename: 'index.html' // output으로 출력할 파일은 index.html 이다.
	}),
	new MiniCssExtractPlugin({
		filename: 'style-test.css'
	})
]
그런 다음 yarn build를 해주신 후 build 디렉터리를 보면 다음과 같이 안쓰는 style.css가 여전히 존재하는 모습을 볼 수 있습니다.



clean-webpack-plugin을 사용해서 사용안하는 파일을 자동으로 삭제할 수 있게 해봅시다!

webpack.config.js를 clean-webpack-plguin을 추가하고 plugins에 적용해 주세요

const CleanWebpackPlugin = require("clean-webpack-plugin");

module.exports = {
 	...,
  plugins: [
    new HtmlWebPackPlugin({
      template: './public/index.html', // public/index.html 파일을 읽는다.
      filename: 'index.html' // output으로 출력할 파일은 index.html 이다.
    }),
    new MiniCssExtractPlugin({
      filename: 'style-test.css'
    }),
    new CleanWebpackPlugin()
  ]
};
그 후 yarn build를 하면 사용 안하는 파일이 삭제된 것을 볼 수 있습니다.
```


### 웹팩 빌드 모드 나누기

```JavaScript
웹팩은 빌드 모드가 Development와 Production에 따라서 차이가 있습니다.

간단하게 설명하면, Development는 빠르게 빌드하기 위해서 빌드할때 최적화를 안하는 특징을 가지고 있고 Production은 빌드할때 최적화 작업을 하고 있습니다.

파일을 confing/webpack.config.dev.js와 config/webpack.config.prod.js로 나누어 적용해 보도록 하겠습니다.

먼저 config 디렉터리를 만드신 후 webpack.config.dev.js와 webpack.config.prod.js를 만들어 주세요

그리고 각 파일들을 아래와 같이 적용해 주세요

config/webpack.config.dev.js

const path = require("path");
const HtmlWebPackPlugin = require("html-webpack-plugin");
const MiniCssExtractPlugin = require("mini-css-extract-plugin");
const CleanWebpackPlugin = require("clean-webpack-plugin");

module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "bundle.js",
    path: path.resolve(__dirname, "../build")
  },
  mode: "development",
  devServer: {
    contentBase: path.resolve(__dirname, "../build"),
    index: "index.html",
    port: 9000
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: "/node_modules",
        use: ["babel-loader"]
      },
      {
        test: /\.html$/,
        use: [
          {
            loader: "html-loader",
            options: { minimize: true }
          }
        ]
      },
      {
        test: /\.css$/,
        use: [MiniCssExtractPlugin.loader, "css-loader"]
      },
      {
        test: /\.scss$/,
        use: [MiniCssExtractPlugin.loader, "css-loader", "sass-loader"]
      }
    ]
  },
  plugins: [
    new HtmlWebPackPlugin({
      template: "./public/index.html",
      filename: "index.html"
    }),
    new MiniCssExtractPlugin({
      filename: "style.css"
    }),
    new CleanWebpackPlugin()
  ]
};
config/webpack.config.prod.js

const path = require("path");
const HtmlWebPackPlugin = require("html-webpack-plugin");
const MiniCssExtractPlugin = require("mini-css-extract-plugin");
const CleanWebpackPlugin = require("clean-webpack-plugin");

module.exports = {
  entry: "./src/index.js",
  output: {
    filename: "bundle.[contenthash].js",
    path: path.resolve(__dirname, "../build")
  },
  mode: "production",
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: "/node_modules",
        use: ["babel-loader"]
      },
      {
        test: /\.html$/,
        use: [
          {
            loader: "html-loader",
            options: { minimize: true }
          }
        ]
      },
      {
        test: /\.css$/,
        use: [MiniCssExtractPlugin.loader, "css-loader"]
      },
      {
        test: /\.scss$/,
        use: [MiniCssExtractPlugin.loader, "css-loader", "sass-loader"]
      }
    ]
  },
  plugins: [
    new HtmlWebPackPlugin({
      template: "./public/index.html",
      filename: "index.html"
    }),
    new MiniCssExtractPlugin({
      filename: "style.css"
    }),
    new CleanWebpackPlugin()
  ]
};
기존 webpack.config.js와 다른점은 mode를 development로 했냐 production으로 했냐에 차이점 입니다.

지금은 별로 차이는 없지만 development와 production에 맞는 플러그인들을 적용하면서 붙여나가기 시작하면 mode에 따라 강점들이 생길 것 입니다!

그 후 package.json에서 스크립트를 다음과 같이 추가해 주세요

"scripts": {
  "start": "webpack-dev-server --config ./config/webpack.config.dev --hot",
  "build": "webpack --config ./config/webpack.config.prod"
 },
이제 yarn start와 yarn build 명령어를 통해서 잘되는지 확인해 보세요!
```