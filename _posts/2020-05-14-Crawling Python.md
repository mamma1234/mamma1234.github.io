---
layout: post
title: "Crawling"
description: 
headline: 
modified: 2020-05-14
category: webdevelopment
imagefeature: cover3.jpg
tags: [Crawling, Scraping, Python, 스크랩핑]
mathjax: 
chart: 
share: true
comments: true
featured: true
disqus:
---


# Crawling

## Web Scraping
HTML, CSS와 같은 웹 페이지에서 구문 분석(Parsing)을 거쳐 필요한 정보를 추출하는 방법

## Web Crawling
정기적으로 특정 웹 사이트를 돌면서 필요한 정보를 수집하는 방법으로, 정기적으로 돌기 때문에 항상 최신 정보를 유지할 수 있습니다.

## requests or urllib(beautifulsoup)
beautifulsoup는 HTML, XML 파일의 정보를 추출해내는 python 라이브러리입니다.

이 방식은 python 내장 모듈인 requests 혹은 urllib을 이용해 HTML를 다운로드 받고, beautifulsoup로 데이터를 추출하는 방식입니다.

이 방식은 서버에서 HTML을 다운로드 받기때문에, 서버사이드렌더링을 사용하지 않는 SPA 사이트나, javascript 렌더링을 필요로하는 사이트들은 크롤링하기가 까다롭습니다.

하지만 사용하기 매우 쉽고, 심플합니다. 멀티프로세스나 멀티스레드를 사용하면 속도도 매우 빠릅니다.

장점 — 쉬움, 심플함, 빠름 (멀티프로세스, 멀티 스레드 적용시 해당)
단점 — javascript 렌더링이 필요한 사이트들을 크롤링하기 어려움. 병렬처리 로직을 별도로 작성하지 않으면 느린편.

HTML 태그를 파싱해서 필요한 데이터만 추출하는 함수를 제공하는 Python 라이브러리로 잘못된 HTML을 수정하여 XML 형식의 Python 객체로 변환합니다.



## Exception
    - 페이지를 혹은 서버를 찾을 수 없는 경우  : HTTPError
    - 존재하지 않는 객체의 태그에 접근한 경우 : AttributeError
```JavaScript
    try:
        html = urlopen(url)
    except HTTPError as e:
        e1 = e
        return e1
    
    try:
        bs0bj = BeautifulSoup(html.read(),'html.parser')
        title = bs0bj.body.h1
    except AttributeError as e:
        e2 = e
        return e2
```



## find(), findall() 