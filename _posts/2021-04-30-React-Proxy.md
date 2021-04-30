---
layout: post
title: "React Proxy"
description: 
headline: 
modified: 2021-04-30
category: webdevelopment
imagefeature: cover3.jpg
tags: [React Proxy]
mathjax: 
chart: 
share: true
comments: true
featured: true
disqus:
---

# Record
## 개념
- 웹팩 갸벌 서버에서 백엔드 API 를 호출 할 때 발생 할 수 있는 CORS 관련 오류를 방지하기 위하여 웹팩 개발 서버에 proxy 를 설정 
- [https://developer.mozilla.org/ko/docs/Web/HTTP/CORS](https://developer.mozilla.org/ko/docs/Web/HTTP/CORS)

## 방법 1
- package.json 에서 proxy 필드를 설정

```JavaScript
{
  "name": "what-is-new",
  "version": "0.1.0",
  ...
  "browserslist": [
    ">0.2%",
    "not dead",
    "not ie <= 11",
    "not op_mini all"
  ],
  "proxy": "https://jsonplaceholder.typicode.com"
}
```

## 방법 2
- 그 중간 단계에서 추가작업을 하고 싶다면, 이 proxy 는 지우고, http-proxy-middleware 라는 모듈을 설치 후 src 디렉토리에 setupProxy.js 라는 파일을 생성

```JavaScript
$ yarn add http-proxy-middleware axios
src/setupProxy.js
const proxy = require('http-proxy-middleware');

module.exports = function(app) {
  app.use(
    proxy('/posts', {
      target: 'http://jsonplaceholder.typicode.com/',
      changeOrigin: true
    })
  );
};

함수 변화 proxy -> createProxyMiddleware

module.exports = function(app) {
  app.use(
    createProxyMiddleware('/posts', {
      target: 'http://jsonplaceholder.typicode.com/',
      changeOrigin: true
    })
  );
};




$ yarn add axios
src/App.js
import React, { Component } from 'react';
import axios from 'axios';

class App extends Component {
  state = {
    data: null
  };
  getPost = async () => {
    try {
      const response = await axios.get('/posts/1');
      this.setState({
        data: response.data
      });
    } catch (e) {
      console.log(e);
    }
  };
  componentDidMount() {
    this.getPost();
  }
  render() {
    if (!this.state.data) {
      return <div>로딩중...</div>;
    }
    const { title, body } = this.state.data;

    return (
      <div>
        <h1>{title}</h1>
        <p>{body}</p>
      </div>
    );
  }
}

export default App;
```




- pathRewrite 설정
```JavaScript
pathRewrite는 서버 API [https://jsonplaceholder.typicode.com/posts/1 이라고 가정했을 때
프론트엔드에서 호출 시에는 API에 특정 URL 규칙을 만들어 가독성을 높이고 싶거나 다수의 proxy를
추가해야 할 업무상 프로세스가 존재할 경우 화면에서 API URL path를 말 그대로 대체해주는 역할을 한다.
아래와 같이 설정할 경우 axios나 fetch 설정 시 /api/posts/1로 호출하게 되면 api는 '' 공백으로 대체되어 호출하게 된다.

// src/setupProxy.js
const proxy = require('http-proxy-middleware');

module.exports = function(app) {
    app.use(
        proxy('/api', {
            target: 'https://jsonplaceholder.typicode.com',
            changeOrigin: true,
            pathRewrite: {
                '^/api': '' // URL ^/api -> 공백 변경
            }
        })
    );
};
```