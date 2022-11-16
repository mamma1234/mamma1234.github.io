---
layout: post
title: 'Node Oracle Client'
description:
headline:
modified: 2020-02-11
category: software platform
imagefeature:
tags: [node oracle client]
mathjax:
chart:
share: true
comments: true
featured: false
disqus:
---

# node-oralce 18.5

## Windows

```JavaScript
    1. oracle client zip 다운로드
    https://www.oracle.com/database/technologies/instant-client/winx64-64-downloads.html

    2. System Path 추가
    C:\oracle\instantclient_18_5\network\admin
```

## Linux Centos7

```JavaScript
    1. oracle client rpm 다운로드
    http://yum.oracle.com/repo/OracleLinux/OL7/oracle/instantclient/x86_64/index.html

    2. yum을 활용하여 oracle client 설치
    yum install -y oracle-instantclient19.3-basic-19.3.0.0.0-1.x86_64.rpm


    Failed dependencies:libaio is needed by oracle-instantclient19.3-basiclite-19.3.0.0.0-1.x86_64
    위와 같은 오류 발생 시

    yum install -y libaio
    위와 같이 라이브러리를 설치해 주면 된다.


    2.  Instant Client를 런타임 링크 경로에 영구적으로 추가
    sudo sh -c "echo /usr/lib/oracle/18.3/client64/lib > /etc/ld.so.conf.d/oracle-instantclient.conf"
    sudo ldconfig



    3. 환경변수 설정
    oracle.sh파일과 .bash_profile에 환경변수를 등록해준다.

    vi /etc/profile.d/oracle.sh

    export ORACLE_HOME=/usr/lib/oracle/19.3/client64
    export TNS_ADMIN=/usr/lib/oracle/19.3/client64/lib/network/admin
    export LD_LIBRARY_PATH=/usr/lib/oracle/19.3/client64/lib
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

## Linux Centos7 Test

```JavaScript
    git clone https://github.com/oracle/node-oracledb.git
    cd node-oracledb
    git checkout dev-2.0
    git submodule init
    git submodule update
    npm install
```

## DPI-1047 "libclntsh.so: cannot open shared object file: No such file or directory"

```JavaScript
DPI-1047: Cannot locate a 64-bit Oracle Client library: "libclntsh.so: cannot open shared object file: No such file or directory". See https://oracle.github.io/odpi/doc/installation.html#linux for help
Node-oracledb installation instructions: https://oracle.github.io/node-oracledb/INSTALL.html
You must have 64-bit Oracle client libraries in LD_LIBRARY_PATH, or configured with ldconfig.
If you do not have Oracle Database on this computer, then install the Instant Client Basic or Basic Light package from
http://www.oracle.com/technetwork/topics/linuxx86-64soft-092277.html



```

-Solution

```JavaScript
cd /usr/lib/oracle/18.3/client64/lib
ln -s libclntsh.so.18.1 libclntsh.so

ENV LD_LIBRARY_PATH="/usr/src/app/oracle/instantclient_18_3/lib"
```

# node-oralce 19.5

```JavaScript
sudo yum install oracle-instantclient19.5-basic-19.5.0.0.0-1.x86_64.rpm

Instant Client 19의 경우 설치 중에 시스템 라이브러리 검색 경로가 자동으로 구성됩니다.

    sudo sh -c "echo /usr/lib/oracle/18.3/client64/lib > /etc/ld.so.conf.d/oracle-instantclient.conf"
    sudo ldconfig
```

# Docker에서 node-oracledb 사용

-   Oracle Linux Instant Client RPM 사용

```JavaScript
FROM oraclelinux:7-slim

RUN  yum -y install oracle-release-el7 && \
     yum-config-manager --enable ol7_oracle_instantclient && \
     yum -y install oracle-instantclient19.5-basiclite && \
     rm -rf /var/cache/yum
```

-   Instant Client zip 파일 자동 다운로드

```JavaScript
RUN wget https://download.oracle.com/otn_software/linux/instantclient/instantclient-basiclite-linuxx64.zip && \
    unzip instantclient-basiclite-linuxx64.zip && rm -f instantclient-basiclite-linuxx64.zip && \
    cd /opt/oracle/instantclient* && rm -f *jdbc* *occi* *mysql* *jar uidrvci genezi adrci && \
    echo /opt/oracle/instantclient* > /etc/ld.so.conf.d/oracle-instantclient.conf && ldconfig


    RUN yum install -y libaio

    RUN apt-get update && apt-get install -y libaio1

```

-   호스트에서 Instant Client zip 파일 복사

```JavaScript

libclntshcore.so.19.1
libclntsh.so.19.1
libnnz19.so
libociicus.so


ADD instantclient_19_5/* /opt/oracle/instantclient_19_5
RUN echo /opt/oracle/instantclient_19_5 > /etc/ld.so.conf.d/oracle-instantclient.conf && \
    ldconfig

    libaio또는 libaio1이전 옵션과 같이 패키지가 필요합니다.
```
