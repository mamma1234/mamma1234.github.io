---
layout: post
title: "Node Oracle"
description: 
headline: 
modified: 2020-02-11
category: webdevelopment
imagefeature: cover3.jpg
tags: [node oracle]
mathjax: 
chart: 
share: true
comments: true
featured: false
disqus:
---

# Windows

```JavaScript
    1. oracle client zip 다운로드
    https://www.oracle.com/database/technologies/instant-client/winx64-64-downloads.html

    2. System Path 추가
    C:\oracle\instantclient_18_5\network\admin
```

# Linux Centos7

```JavaScript
    1. oracle client rpm 다운로드
    http://yum.oracle.com/repo/OracleLinux/OL7/oracle/instantclient/x86_64/index.html

    2. yum을 활용하여 oracle client 설치
    yum install -y oracle-instantclient19.3-basic-19.3.0.0.0-1.x86_64.rpm


    Failed dependencies:libaio is needed by oracle-instantclient19.3-basiclite-19.3.0.0.0-1.x86_64
    위와 같은 오류 발생 시

    yum install -y libaio
    위와 같이 라이브러리를 설치해 주면 된다.



    3. 환경변수 설정
    oracle.sh파일과 .bash_profile에 환경변수를 등록해준다.

    vi /etc/profile.d/oracle.sh

    export ORACLE_HOME=/usr/lib/oracle/19.3/client64
    export TNS_ADMIN=/usr/lib/oracle/19.3/client64/bin
    oracle.sh파일에는 client 설치 경로를 설정한다.


    vi ~/.bash_profile 

    # .bash_profile
    # Get the aliases and functions
    if [ -f ~/.bashrc ]; then
    . ~/.bashrc
    fi
    # User specific environment and startup programs
    PATH=$PATH:$HOME/bin:$ORACLE_HOME/bin 
    export PATH
    .bash_profile 파일에는 ORACLE_HOME을 추가한다.
```