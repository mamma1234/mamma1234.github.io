---
layout: post
title: "Spring Cloud Gateway"
description: 
headline: 
modified: 2020-10-23
category: webdevelopment
imagefeature: cover3.jpg
tags: [Spring Cloud Gateway]
mathjax: 
chart: 
share: true
comments: true
featured: true
disqus:
---

# Spring Cloud Gateway
-  Spring 5, Spring Boot 2 및 Project Reactor를 포함하여 Spring Ecosystem 위에 구축 된 API Gateway를 제공합니다. Spring Cloud Gateway는 API로 라우팅하는 간단하면서도 효과적인 방법을 제공하고 보안, 모니터링 / 메트릭 및 탄력성과 같은 교차 절단 문제를 제공하는 것을 목표

[https://cloud.spring.io/spring-cloud-gateway/reference/html] (https://cloud.spring.io/spring-cloud-gateway/reference/html/)

# 용어
## Route : Route 는 Gateway 를 이루는 기본 단위. ID 로 정의되며, 도착 URI, predicate 들과 filter 들의 모음이다. predicate 가 모두 충족되면 Route 가 매칭된다.
## Predicate : Java8 Function Predicate 이다. Input 타입은 Spring Framework 의 ServerWebExchange 이다. Header 와 Parameter 와 같은 HTTP 구성 요소들로 개발자가 Matching 여부를 판단할 수 있도록 도와준다.
## Filter : Spring Framework 의 GatewayFilter 이다. downstream 으로 요청을 보내기 전과 후에 Request 와 Response 를 수정할 수 있게 해준다.