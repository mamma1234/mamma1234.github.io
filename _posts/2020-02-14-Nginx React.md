---
layout: post
title: "React를 Nginx웹 서버에 배포하기"
description: 
headline: 
modified: 2020-02-14
category: webdevelopment
imagefeature: cover3.jpg
tags: [React Nginx]
mathjax: 
chart: 
share: true
comments: true
featured: false
disqus:
---
# Nginx
## Windows
```
C:\github\mamma1234\nginx-1.17.8\conf\nginx.conf

    server {
        listen       80;
        server_name  localhost;

        #charset koi8-r;

        #access_log  logs/host.access.log  main;

        location / {
            root   C:\github\mamma1234\klnet.owner\klnet.owner.web\material-react-mobx\build;
            index  index.html index.htm menu.html;
            try_files $uri $uri/ /index.html;
        }


```

## 기본 파일, 폴더
- sites-available : 가상 서버 환경들에 대한 설정 파일들이 위치하는 부분입니다. 가상 서버를 사용하거나 사용하지 않던간에 그에 대한 설정 파일들이 위치하는 곳이다.
- sites-enabled : sites-available 에 있는 가상 서버 파일들중에서 실행시키고 싶은 파일을 symlink로 연결한 폴더입니다. 실제로 이 폴더에 위치한 가상서버 환경 파일들을 읽어서 서버를 세팅합니다.
- nginx.conf : Nginx에 관한 설정파일로 Nginx 설정에 관한 블록들이 작성되어 있으며 이 파일에서 sites-enabled 폴더에 있는 파일들을 가져옵니다.

