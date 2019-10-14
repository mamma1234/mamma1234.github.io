---
layout: post
title: "CLI"
description: 
headline: 
modified: 2019-10-10
category: webdevelopment
imagefeature: cover3.jpg
tags: [CLI]
mathjax: 
chart: 
share: true
comments: true
featured: true
disqus:
---

# Record
## 개념
명령어 기반 인터페이스 도구(CLI)
CLI (Command Line Interface)



## 핵심 개념
- Git Bash

- WebPack CLI
npm i -g webpack-cli

-git init
-git add *
-git commit -m "first commit"
-git remote add origin https://github.com/juliusds/
-g-it push -u origin master


-git init
-git status
-git add test.txt 
-git config --global user.name '이름'
-git config --globall user.email '이메일'
-git commit 
-git log  
-git log -p
-git diff 커밋ID1..커밋ID2
-git reset 커밋ID --hard
-git revert 
-git branch test_1 -브랜치 생성
-git checkout test_1 -브랜치 선택
-git log master..test_1 -p   -브랜치 간에 차이 확인
-git diff master..test_1
-git log --branches --decorate --graph (--oneline)
-git checkout master
-git checkout -b test_2   -> test_2 브랜치를 생성하고 체크아웃한다.
-git branch -d test_2  -> test_2 브랜치를 삭제한다.
-fast-forward 커밋을 생성하지 않는다.
-3wayMerge -> 커밋 내용이 다른 두 브랜치를 병합하는 방법, 새로운 커밋 생성
-git stash apply 임시 저장한 작업 내용을 다시 불러옴
-stree   -> 현재 프로젝트의 버전 관리를 소스트리에서 보여줌  