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

### requests or urllib(beautifulsoup)
beautifulsoup는 HTML, XML 파일의 정보를 추출해내는 python 라이브러리입니다.

이 방식은 python 내장 모듈인 requests 혹은 urllib을 이용해 HTML를 다운로드 받고, beautifulsoup로 데이터를 추출하는 방식입니다.

이 방식은 서버에서 HTML을 다운로드 받기때문에, 서버사이드렌더링을 사용하지 않는 SPA 사이트나, javascript 렌더링을 필요로하는 사이트들은 크롤링하기가 까다롭습니다.

하지만 사용하기 매우 쉽고, 심플합니다. 멀티프로세스나 멀티스레드를 사용하면 속도도 매우 빠릅니다.

장점 — 쉬움, 심플함, 빠름 (멀티프로세스, 멀티 스레드 적용시 해당)
단점 — javascript 렌더링이 필요한 사이트들을 크롤링하기 어려움. 병렬처리 로직을 별도로 작성하지 않으면 느린편.

HTML 태그를 파싱해서 필요한 데이터만 추출하는 함수를 제공하는 Python 라이브러리로 잘못된 HTML을 수정하여 XML 형식의 Python 객체로 변환합니다.


### scrapy
Scrapy는 크롤링을 위해 개발된 프레임워크입니다.
API 및 클래스를 이용한 웹 데이터 수집 라이브러리

미들웨어, 파이프라인, javascript renderer(splash), proxy, xpath, CLI 등 다양한 기능들과 플러그인들을 사용할 수 있습니다.

병렬처리, robots.txt 준수 여부, 다운로드 속도 제어등도 설정할 수 있습니다.

장점 — 다양한 플러그인 보유, 훌륭한 커뮤니티와 문서화, 크롤링에 필요한 다양한 기능
단점 — 플러그인들끼리 서로 호환이 안되는 경우가 있을 수 있음.


웹사이트를 크롤링 및 스크래핑을 통해 정보를 추출하고, 이를 데이터셋의 형태로 저장하는데 특화된 라이브러리

*문제 : 기초적인 기능만 사용하면, 보고있는 화면을 그대로 스크래핑 할 수 없다. ex> 동적 웹 페이지, 요청시 로그인 정보 함께 보내는 웹 페이지
(ex1) https://www.premierleague.com/tables?co=1&se=42&mw=-1&ha=-1 사이트의 경우
처음에는, 기본적인 정적 웹 페이지(html/css로만 구성)을 띄운 다음, 곧바로 사용자 요청에 의해 드랍박스대로 서버에 요청해서 동적으로 웹페이지가 바뀐다. 만약 여기서 Scrapy만 사용한다면, 처음 잠시 띄워진 정적웹페이지만을 가져온다는 단점이 있다.

(ex2) 로그인 정보를 한꺼번에 보내야하는 웹 페이지의 경우이다.  회원에게 제공되는 웹페이지를 보고 싶을 때, 현재 회원정보로 로그인 되어있다는 정보를 함께 보내야한다. 이것을 전문용어로 쿠키라 한다.
로그인한 상태에서는 메뉴와 강의듣기가 달라진다.(로그인 전 에는 로그인하라고 페이지가 뜬다)
이것은, 요청시, 서버에 쿠키를 같이 보냈기 때문이다.
만약 여기서 Scrapy만 사용한다면, url에 쿠키를 같이 보낼 수 없다.


### selenium
Selenium은 웹 자동화 테스트 (버튼 클릭, 스크롤 조작 등등)에 사용되는 프레임워크입니다.

셀레니움을 이용한 크롤러는 웹 페이지에서 javascript 렌더링을 통해 생성되는 데이터들을 손쉽게 가져올 수 있습니다.

인터넷 브라우저를 통해 크롤링을 하는 개념이라, 실제 보여지는 웹페이지의 전부를 가져올 수 있고, 디버깅 방법또한 직관적입니다.

하지만 웹 브라우저를 실제로 실행시키는 방법이기 때문에 속도도 많이 느리고, 메모리도 상대적으로 많이 차지합니다.

멀티프로세스를 사용해서 여러 브라우저로 크롤링하도록 하면 속도를 일정부분 개선할 수 있습니다.

팁으로 셀레니움을 사용하실 때 Docker를 사용하시면 매우 편리합니다(특히 headless 모드로 크롤링할 때 리소스 정리가 매우 쉽습니다)

장점 — 사용자가 보는 웹 페이지의 모든 정보를 가져올 수 있음, javascript rendering 기능 지원, 사용방법이 직관적이고 쉬움.
단점 — 느림, 메모리를 많이 차지.

Selenium에서 제공하는 webdriver 모듈을 사용하여, 동적 웹페이지나 로그인정보를 담아 서버에 요청하는 작업을 할 수 있게 한다.
Scrapy 기초기능의 단점을 보완한다.(고급기능까지 쓰면 되지만, html/css/js의 이해도가 필요하다)


```JavaScript
from selenium import webdriver
browser = webdriver.Chrome("C:\\github\\chromedriver.exe")
browser.get("http://asdfkakd.com")
browser.quit()
```

### why
웹 크롤링 및 스크래핑을 위한 Python 라이브러리 : Scrapy
파이썬 웹브라우저 자동화 라이브러리 : Selenium


Scrapy 웹사이트를 크롤링 및 스크래핑을 통해 정보를 추출하고, 이를 데이터셋의 형태로 저장하는데 특화된 라이브러리

*문제 : 기초적인 기능만 사용하면, 보고있는 화면을 그대로 스크래핑 할 수 없다. ex> 동적 웹 페이지, 요청시 로그인 정보 함께 보내는 웹 페이지
(ex1) https://www.premierleague.com/tables?co=1&se=42&mw=-1&ha=-1 사이트의 경우
처음에는, 기본적인 정적 웹 페이지(html/css로만 구성)을 띄운 다음, 곧바로 사용자 요청에 의해 드랍박스대로 서버에 요청해서 동적으로 웹페이지가 바뀐다. 만약 여기서 Scrapy만 사용한다면, 처음 잠시 띄워진 정적웹페이지만을 가져온다는 단점이 있다.

(ex2) 로그인 정보를 한꺼번에 보내야하는 웹 페이지의 경우이다.  회원에게 제공되는 웹페이지를 보고 싶을 때, 현재 회원정보로 로그인 되어있다는 정보를 함께 보내야한다. 이것을 전문용어로 쿠키라 한다.
로그인한 상태에서는 메뉴와 강의듣기가 달라진다.(로그인 전 에는 로그인하라고 페이지가 뜬다)
이것은, 요청시, 서버에 쿠키를 같이 보냈기 때문이다.
만약 여기서 Scrapy만 사용한다면, url에 쿠키를 같이 보낼 수 없다.

Selenium에서 제공하는 webdriver 모듈을 사용하여, 동적 웹페이지나 로그인정보를 담아 서버에 요청하는 작업을 할 수 있게 한다.
Scrapy 기초기능의 단점을 보완한다.(고급기능까지 쓰면 되지만, html/css/js의 이해도가 필요하다)



## install
```JavaScript
python -m venv venv
venv\Scripts\activate
pip install scrapy
pip install selenium
pip install beautifulsoup4
scrapy startproject myscrapy1
(test) scrapy shell https://www.geeksforgeeks.org/
(test) view(response)
(test) print(response.text)

(test) scrapy genspider mybots "news.naver.com/main/list.nhn?mode=LS2D&mid=shm&sid1=105&sid2=732"

scrapy startproject myscrapy1
scrapy genspider mybots "news.naver.com/main/list.nhn?mode=LS2D&mid=shm&sid1=105&sid2=732"
(scrapy genspider {파일이름} {url} 입력)

myscrapy1 - settings.py
scrapy crawl mybots




```

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

https://blog.naver.com/PostView.nhn?blogId=altmshfkgudtjr&logNo=221494904057&from=search&redirect=Log&widgetTypeCall=true&directAccess=false
