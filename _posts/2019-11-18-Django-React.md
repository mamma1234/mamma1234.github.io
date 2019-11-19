---
layout: post
title: "Django React"
description: 
headline: 
modified: 2019-11-18
category: webdevelopment
imagefeature: cover3.jpg
tags: [Django, React]
mathjax: 
chart: 
share: true
comments: true
featured: true
disqus:
---

# Record
## 개념
- python3.x + django + djangorestframework

## python3
### 가상환경
- (가상환경 생성) python -m venv django-react-venv
파이썬에서는 한 라이브러리에 대해 하나의 버전만 설치가 가능합니다.
여러개의 프로젝트를 진행하게 되면 이는 문제가 됩니다. 작업을 바꿀때마다 다른 버전의 라이브러리를 설치해야합니다.
이를 방지하기 위한 격리된 독립적인 가상환경을 제공합니다.
일반적으로 프로젝트마다 다른 하나의 가상환경을 생성한 후 작업을 시작하게 됩니다.

- (가상환경 실행) django-react-venv\Scripts\activate
- (가상환경 종료) deactivate

### PIP
- (PIP 설치) python -m pip install --upgrade pip
파이썬으로 작성된 패키지 소프트웨어를 설치, 관리하는 시스템

### Django
- (Django 설치) pip install django

### Django 프로젝트 만들기
- (Django Admin 설치) django-admin startproject djangoreactapi .

### Python manage.py
- python manage.py startapp post
django 프로젝트 하위 앱 생성
- python manage.py makemigrations
마이그레이션 준비
- python manage.py migrate 
데이터베이스에 기본 테이블 생성(Groups, Users)
- python manage.py runserver
장고 테스트용 웹서버 실행
- python manage.py createsuperuser 
장고 어드민 사이트의 관리자 생성
- python manage.py shell
파이썬 쉘모드 실행
- python manage.py collectstatic
정적자원(css, html등) 재수집(동기화)
- python manage.py test
TestCase를 상속받은 테스트코드 실행
- python manage.py clearsessions
sessions 클리어

### django-rest-framework 설치
- pip install djangorestframework


### Same-origin policy 추가
- pip install django-cors-headers
api를 통한 데이터의 접근제어를 위해 HTTP 접근제어 규약(CORS : Cross-Origin Resource Sharing)을 추가
CORS_ORIGIN_WHITELIST = ['http://localhost:3000']




선언형 뷰는 코드를 예측 가능하고 디버그하기 쉽게 만듭니다.

### 컴포넌트 기반
스스로 상태를 가지고 관리하는 캡슐화된 컴포넌트를 생성한 다음 복잡한 UI를 만들기 위해 구성합니다.

컴포넌트 로직은 템플릿 대신 JavaScript로 작성되므로, 앱을 통해 풍부한 데이터를 쉽게 전달하고 DOM에서 상태를 유지할 수 있습니다.

### 한번 배우고, 어디서나 작성한다
기술 스택의 나머지 부분에 대해 가정하지 않으므로, 기존 코드를 다시 작성하지 않고 React에서 새로운 기능을 개발할 수 있습니다.

React는 React Native를 이용하여 강력한 모바일앱을 만들거나 Node를 사용한 서버에서 렌더링할 수도 있습니다.

#### React
- JSX : JavaScript를 확장한 문법
- props : props 는 부모 컴포넌트가 자식 컴포넌트에게 주는 값.  props 를 직접 수정 할 수 는 없습니다.
- state : state 는 컴포넌트 내부에서 선언하며 내부에서 값을 변경 할 수 있습니다.
- flow
![]({{ site.url }}/images/react_flow.jpeg)
- Life Cycle
![]({{ site.url }}/images/react_lifecyle.png)