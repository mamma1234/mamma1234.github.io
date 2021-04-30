---
layout: post
title: "Service Worker"
description: 
headline: 
modified: 2021-04-30
category: webdevelopment
imagefeature: cover3.jpg
tags: [Service Worker]
mathjax: 
chart: 
share: true
comments: true
featured: true
disqus:
---

# Record
## 개념
- 풍부한 오프라인 경험, 주기적 백그라운드 동기화, 푸시 알림(일반적으로
원시 애플리케이션을 요구하는 기능)이 웹에서 지원되고 있습니다.
서비스 워커는 이러한 모든 기능의 기술적 기반을 제공합니다


- 서비스워커는 브라우저가 백그라운드에서 실행하는 스크립트로, 웹페이지와는 별개로 작동하며 웹페이지 또는 사용자의 인터랙션이 필요하지 않은 기능만 제공하고 있습니다.
서비스워커의 수명 주기는 웹페이지와는 완전히 별개입니다. 웹 서비스와 브라우저 및 네트워크 사이에서 프록시 서버의 역할을 하며, 오프라인에서도 서비스를 사용할 수 있도록 합니다.
  웹 페이지와 별개로 존재하기 때문에 다음과 같은 제약이 있습니다.
  서비스워커는 요청하지 않는 이상, 없는 것이나 다름없습니다. Web Worker에서와 같은 .ternimate() 명령은 존재하지 않습니다.
  웹 페이지 life cycle을 따르지 않습니다. 서비스워커는 웹페이지가 닫히더라도 자동으로 비활성화되지 않습니다.
  웹 페이지와 별개로 존재하므로 DOM이나 window요소에 접근할 수 없습니다.


## 참조

- [https://berkbach.com/service-worker-%EC%97%90-%EA%B4%80%ED%95%B4%EC%84%9C-9c8f9f2f3988](https://berkbach.com/service-worker-%EC%97%90-%EA%B4%80%ED%95%B4%EC%84%9C-9c8f9f2f3988)

- [https://so-so.dev/web/service-worker/](https://so-so.dev/web/service-worker/)


1. 캐시와 상호작용
2. 푸쉬 알림
3. 백그라운드 동기화

