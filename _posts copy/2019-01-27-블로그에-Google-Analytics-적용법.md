---
layout: post
title: "Jekyll Github 블로그에 Google Analytics 적용법"
description: 
headline: 
modified: 2019-01-27
category: webdevelopment
tags: [blog, github, jekyll]
imagefeature: 
mathjax: 
chart: 
share: true
comments: true
---

Gitbub 블로그를 운영하면 방문자의 수를 기본적으로는 알기 힘들다. 이때 [Google Analytics](https://analytics.google.com/)를 적용하면 블로그 방문자 추적을 상세하게 할 수 있다.

먼저 [Google Analyticss](https://analytics.google.com/)에 가입하자, 만약 Google 계정 등이 있다면 더 간단하게 회원가입을 할 수 있다.

![]({{ site.url }}/images/ga1.JPG)  
먼저 필요한 정보들과 자신의 블로그 URL을 기재한다.

![]({{ site.url }}/images/ga2.JPG)  
국가는 우리나라로 설정하고

![]({{ site.url }}/images/ga3.JPG)  
`Get Tracking ID`를 클릭한다.

![]({{ site.url }}/images/ga4.JPG)  
약관 동의를 하고 나면 이제 추적을 시작할 수 있다.

![]({{ site.url }}/images/ga5.JPG)  
Tracking ID를 복사해서

![]({{ site.url }}/images/ga8.JPG)  
`_config` 파일에 `google_analytics`부분에 붙여 넣는다.

![]({{ site.url }}/images/ga6.JPG)  
그리고 `Global Site Tag`부분을 복사해서

![]({{ site.url }}/images/ga7.JPG)  
`_includes`폴더에 `scripts.html`파일 하단에 붙여넣기를 한다.  

저장 후 `git pull`을 진행하고 [Google Analyticss](https://analytics.google.com/) `Real-Time`에 `Overview`에 들어가면 추적 내용을 확인할 수 있다. 

![]({{ site.url }}/images/ga9.JPG) 

![]({{ site.url }}/images/ga.png) 

![]({{ site.url }}/images/ga2.GIF) 
