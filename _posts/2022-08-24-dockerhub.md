---
layout: post
title: 'dockerhub'
description:
headline:
modified: 2022-08-24
category: webdevelopment
imagefeature:
tags: [dockerhub]
mathjax:
chart:
share: true
comments: true
featured: true
disqus:
---

# Record

## 목차

-   [](#)

## 개념

[https://hub.docker.com](https://hub.docker.com/)

### docker push 에러 (denied: requested access to the resource is denied)

-   Docker Hub 로그인을 하지 않음
-   Docker Hub 아이디와 태그된 이미지의 이름이 일치하지 않음
    -   Docker Tag 를 Docker Hub ID 와 동일하게 생성합니다.

```
    $ docker tag kubia bcp0109/kubia
```
