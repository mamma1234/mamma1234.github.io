---
layout: post
title: 'Logispot-개발-환경-셋팅'
description:
headline:
modified: 2022-03-04
category: webdevelopment
imagefeature:
tags: [Logispot-개발-환경-셋팅]
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

-

## 설치

-   git

```JavaScript
git clone git@github.com:mamma1234/logispot.git

git remote add upstream https://github.com/Logispot/logispot.git


git clone git@github.com:mamma1234/logispot-client-ios.git

git remote add upstream https://github.com/Logispot/logispot-client-ios.git


git clone git@github.com:mamma1234/logispot-driver-ios.git

git remote add upstream https://github.com/Logispot/logispot-driver-ios.git


git clone git@github.com:mamma1234/logispot-driver-android.git

git remote add upstream https://github.com/Logispot/logispot-driver-android.git


git clone git@github.com:mamma1234/logispot-client-android.git

git remote add upstream https://github.com/Logispot/logispot-client-android.git
```

-   PHP 초기화

```JavaScript
$ brew update
$ brew upgrade
$ brew cleanup

$ brew list | grep php

$ brew uninstall --force php56 php56-apcu php56-opcache php56-xdebug php56-yaml
$ brew uninstall --force php70 php70-apcu php70-opcache php70-xdebug php70-yaml
$ brew uninstall --force php71 php71-apcu php71-opcache php71-xdebug php71-yaml
$ brew uninstall --force php72 php72-apcu php72-opcache php72-xdebug php72-yaml

$ brew cleanup

마지막으로 이전에 저장된 설정파일도 모두 지우도록 하겠습니다.

$ rm -Rf /usr/local/etc/php/*
```

-   PHP 7.2 설치 문제

```JavaScript
brew tap shivammathur/php
brew install shivammathur/php/php@7.2
```

-   symbolic link
    sudo ln ../logispot logispot_local

-   composer install 문제

```JavaScript
docker

Problem 1
    - Root composer.json requires PHP extension ext-ssh2 * but it is missing from your system. Install or enable PHP's ssh2 extension.

apt-get install libssh2-1 php-ssh2 -y
mkdir alternatives
    debconf: unable to initialize frontend: Dialog
    Creating config file /etc/php/7.2/phpdbg/php.ini with new version

일부 설치 오류나지만 무시


composer install 재시도





flAbsPath on /var/lib/dpkg/status failed - realpath (2: No such file or directory
mkdir dpkg
vi status
apt-get update


apt-get -y install sudo

debconf: delaying package configuration, since apt-utils is not installed
dpkg: error: cannot scan updates directory '/var/lib/dpkg/updates/': No such file or directory


dpkg: error: unable to create new file '/var/lib/dpkg/info/format-new': No such file or directory

```

##

pecl install xdebug

/etc/php/7.2/cli/php.ini

zend_extension="xdebug.so"
xdebug.log="/var/www/path_to_log/xdebug.log"
xdebug.mode=develop,debug
xdebug.client_port=9003
xdebug.start_with_request=yes
xdebug.discover_client_host=1
xdebug.client_host=host.docker.internal

# xdebug.client_host=localhost

xdebug.output_dir="/var/www/path_to_log/"

## 로그

tail -f /Users/parkdaekyu/Desktop/project/phpstormProjects/logispot/storage/logs/laravel.log

cd /var/log/nginx

/Users/parkdaekyu/Desktop/project/phpstormProjects/logispot/storage/logs/sql-2022-03-17.log

/Users/parkdaekyu/Desktop/project/logispot-docker/logispot_local/path_to_log/xdebug.log

/Users/parkdaekyu/Desktop/project/phpstormProjects/logispot/storage/logs/woker.log

## db 날짜 변경 (미완)

SET time_zone='Asia/Seoul';

SET GLOBAL time_zone='Asia/Seoul';

## say 070 api 호출되는거 끄는 법 좀 알려주세요

https://pbx140.fn070.com:8002/socket.io/?EIO=3&transport=polling&t=N-mMifL

extensions 테이블에서 사용하고 계시는 user_carrier_id 찾으셔서 delete하시고 재로그인하시면되요

delete from extensions where user_carrier_id = 7

##

```JavaScript
//app/Providers/AppServiceProvider.php
    public function register()
    {
        //daekyu.park debug..
        if ($this->app->environment() !== 'production') {
            \Event::listen('Illuminate\Database\Events\QueryExecuted', function ($query) {
                \Log::channel('sql')->info([
                    'sql' => $query->sql,
                    'bindings' => $query->bindings,
                    'time' => $query->time,
                ]);
            });
        }
    }
//config/logging.php
        //daekyu.park debug..
        'sql' => [
            'driver' => 'daily',
            'path' => storage_path('logs/sql.log'),
            'level' => 'debug',
            'days' => 14,
        ],



{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [

        {
            "name": "Listen for Xdebug 2 (Legacy)",
            "type": "php",
            "request": "launch",
            "port": 9000,
            "runtimeExecutable" : "/usr/local/opt/php@7.2/bin/php"
        },

        {
            "name": "Launch currently open script",
            "type": "php",
            "request": "launch",
            "program": "${file}",
            "cwd": "${fileDirname}",
            "port": 9000,
            "runtimeArgs": [
                "-dxdebug.start_with_request=yes"
            ],
            "env": {
                "XDEBUG_MODE": "debug,develop",
                "XDEBUG_CONFIG": "client_port=${port}"
            }
        },
        {
            "name": "Listen for Xdebug",
            "type": "php",
            "request": "launch",
            "hostname":"localhost",
            // "hostname":"host.docker.internal",
            "port": 9003,
            "pathMappings": {
                "/var/www": "${workspaceFolder}"
            }
        },
    ]
}


```

## DB 커넥트

ssh logispot@13.125.23.155 -L 3101:logispot-prod.cnii1tftmuzr.ap-northeast-2.rds.amazonaws.com:3306

foreground: logispot@13.125.23.155
background: logispot@54.180.182.73

ssh ddasi@192.168.0.250 -p 22 -L 10022:123.123.123.123:22

## docker php unit

ln -sf /var/www/vendor/bin/phpunit /usr/local/bin/phpunit

## 라우트 오류 발생시

php artisan optimize , cache:clear, route:clear , config:clear

## AWS 셋팅

DB_CONNECTION=mysql
DB_HOST= logispot-prod.cnii1tftmuzr.ap-northeast-2.rds.amazonaws.com
DB_HOST_READONLY= logispot-prod-readonly.cnii1tftmuzr.ap-northeast-2.rds.amazonaws.com
DB_HOST_READONLY_2=logispot-prod-readonly.cnii1tftmuzr.ap-northeast-2.rds.amazonaws.com
DB_PORT=3306
DB_DATABASE=logispot_prod
DB_USERNAME=logispot
DB_PASSWORD=1t1c$HRGvbEW
DB_HOST_FOR_INFLUXDB=ip-172-31-30-71.ap-northeast-2.compute.internal
DB_USERNAME_FOR_INFLUXDB=logispot
DB_PASSWORD_FOR_INFLUXDB=Wd3wAb4SK2SdpBKQ

ssh logispot@13.125.23.155 -L 3101:logispot-prod.cnii1tftmuzr.ap-northeast-2.rds.amazonaws.com:3306
ssh logispot@13.125.23.155 -L 3102:logispot-prod-readonly.cnii1tftmuzr.ap-northeast-2.rds.amazonaws.com:3306

ssh ubuntu@13.209.22.247
## 운영 Vue webpack compile

~/www/releases/current$ npm run production
