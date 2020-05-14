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
- python manage.py runserver
파이썬 서버 구동


### django-rest-framework 설치
- pip install djangorestframework


### Same-origin policy 추가
- pip install django-cors-headers
api를 통한 데이터의 접근제어를 위해 HTTP 접근제어 규약(CORS : Cross-Origin Resource Sharing)을 추가
CORS_ORIGIN_WHITELIST = ['http://localhost:3000']

### 참고 사이트
[참고](https://this-programmer.com/entry/%EA%B0%84%EB%8B%A8%ED%95%9C-react-JS-Django-%EC%96%B4%ED%94%8C%EB%A6%AC%EC%BC%80%EC%9D%B4%EC%85%98-%EB%A7%8C%EB%93%A4%EA%B8%B0)


