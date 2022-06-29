---
layout: post
title: 'node Express'
description:
headline:
modified: 2020-01-16
category: webdevelopment
imagefeature:
tags: [Express]
mathjax:
chart:
share: true
comments: true
featured: true
disqus:
---

# Express

## Introduction

## express

app.set
app.use
app.listen
app.get
app.post

## 패키지

morgan: 요청에 대한 정보를 콘솔에 기록
cookie-parser: 요청에 동봉된 쿠키를 해석
static: 정적인 파일을 제공, public 폴더에 정적 폴더를 넣는다.
express-session: 세션 관리용 미들웨어, 로그인 드의 이유로 세션을 구현할 때 유용하다.
connect-flash: 일회성 메시지들을 웹 브라우저에 나타낼 때 사용한다. cookie-parser와 express-session 뒤에 위치해야한다.
에러 처리 미들웨어: error라는 템플릿 파일을 렌더링한다. 404에러가 발생하면 404처리 미들웨어에서 넣어준 값을 사용한다.
bcrypt: 모듈의 hash 메서드를 사용하면 쉽게 암호화 할 수 있다. bcrypt의 두번째 인자는 12 이상 숫자를 추천한다. 숫자가 커질수록 비밀번호를 알아내기 어렵지만 암호화 시간도 오래 걸린다. 31까지 사용 가능하다.
Passport :

body-parser : JSON과 URL-encoded 형식의 본문 외에도 Raw, Text형식의 본문을 추가로 해석할 수 있다.
예를 들어 JSON 형식으로 { name: 'backback' , book: 'nodejs' }를 본문으로 보낸다면 req.body에 그대로 들어간다.

-   URL-encoded 형식으로 name=backback&book=node.js를 본문으로 보낸다면
-   req.body에 { name : 'backback' , book: 'nodejs' }가 들어간다.
    body-parser가 모든 본문을 해석해주는 것은 아니다.
    multipart/form-data 같은 폼을 통해 전송된 데이터는 해석하지 못한다.
