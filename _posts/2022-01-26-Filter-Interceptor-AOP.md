---
layout: post
title: "Git"
description: 
headline: 
modified: 2022-01-26
category: webdevelopment
imagefeature: cover3.jpg
tags: [GFilter, Interceptor, AOPit]
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

## 목차
- [](#)

## Filter, Interceptor, AOP 의 흐름
ㆍInterceptor와 Filter는 Servlet 단위에서 실행된다. <> 반면 AOP는 메소드 앞에 Proxy패턴의 형태로 실행된다.
ㆍ실행순서를 보면 Filter가 가장 밖에 있고 그안에 Interceptor, 그안에 AOP가 있는 형태이다.
따라서 요청이 들어오면 Filter → Interceptor → AOP → Interceptor → Filter 순으로 거치게 된다.
