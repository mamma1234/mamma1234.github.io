---
layout: post
title: 'CLI'
description:
headline:
modified: 2019-10-10
category: CI/CD
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

-   Git Bash

-   WebPack CLI
    npm i -g webpack-cli

-git init
-git add \*
-git commit -m "first commit"
-git remote add origin https://github.com/juliusds/
-git push -u origin master

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
-git log master..test_1 -p -브랜치 간에 차이 확인
-git diff master..test_1
-git log --branches --decorate --graph (--oneline)
-git checkout master
-git checkout -b test_2 -> test_2 브랜치를 생성하고 체크아웃한다.
-git branch -d test_2 -> test_2 브랜치를 삭제한다.
-fast-forward 커밋을 생성하지 않는다.
-3wayMerge -> 커밋 내용이 다른 두 브랜치를 병합하는 방법, 새로운 커밋 생성
-git stash apply 임시 저장한 작업 내용을 다시 불러옴
-stree -> 현재 프로젝트의 버전 관리를 소스트리에서 보여줌

## git 취소하기

git add를 취소할 수 있다.
git commit을 취소할 수 있다.
git push를 취소할 수 있다.
untracked 파일을 삭제할 수 있다.

### git add 취소하기(파일 상태를 Unstage로 변경하기)

-   아래와 같이 실수로 git add \* 명령을 사용하여 모든 파일을 Staging Area에 넣은 경우,
-   Staging Area(git add 명령 수행한 후의 상태)에 넣은 파일을 빼고 싶을 때가 있다.

```JavaScript
    // 모든 파일이 Staged 상태로 바뀐다.
    $ git add *
    // 파일들의 상태를 확인한다.
    $ git status
    On branch master
    Changes to be committed:
    (use "git reset HEAD <file>..." to unstage)
    renamed:    README.md -> README
    modified:   CONTRIBUTING.md
    https://gmlwjd9405.github.io/2018/05/25/git-add-cancle.html
```

이때, git reset HEAD [file] 명령어를 통해 git add를 취소할 수 있다.

-   뒤에 파일명이 없으면 add한 파일 전체를 취소한다.
-   CONTRIBUTING.md 파일을 Unstaged 상태로 변경해보자.

```JavaScript
// CONTRIBUTING.md 파일을 Unstage로 변경한다.
$ git reset HEAD CONTRIBUTING.md
Unstaged changes after reset:
M	CONTRIBUTING.md
```

```JavaScript
// 파일들의 상태를 확인한다.
$ git status
On branch master
Changes to be committed:
(use "git reset HEAD <file>..." to unstage)
  renamed:    README.md -> README
Changes not staged for commit:
(use "git add <file>..." to update what will be committed)
(use "git checkout -- <file>..." to discard changes in working directory)
  modified:   CONTRIBUTING.md
```

### git commit 취소하기

#### commit 취소하기

-   완료한 commit을 취소해야 할 때가 있다.
    너무 일찍 commit한 경우
    어떤 파일을 빼먹고 commit한 경우 이때, git reset HEAD^ 명령어를 통해 git commit을 취소할 수 있다.

        - 너무 일찍 commit한 경우
        - 어떤 파일을 빼먹고 commit한 경우 이때, git reset HEAD^ 명령어를 통해 git commit을 취소할 수 있다.

```JavaScript
// commit 목록 확인
$ git log
```

```JavaScript
// [방법 1] commit을 취소하고 해당 파일들은 staged 상태로 워킹 디렉터리에 보존
$ git reset --soft HEAD^
// [방법 2] commit을 취소하고 해당 파일들은 unstaged 상태로 워킹 디렉터리에 보존
$ git reset --mixed HEAD^ // 기본 옵션
$ git reset HEAD^ // 위와 동일
$ git reset HEAD~2 // 마지막 2개의 commit을 취소
// [방법 3] commit을 취소하고 해당 파일들은 unstaged 상태로 워킹 디렉터리에서 삭제
$ git reset --hard HEAD^
```

#### commit message 변경하기

-   commit message를 잘못 적은 경우, git commit –amend 명령어를 통해 git commit message를 변경할 수 있다.

```JavaScript
$ git commit --amend
```

-   TIP git reset 명령은 아래의 옵션과 관련해서 주의하여 사용해야 한다.
    reset 옵션
    –soft : index 보존(add한 상태, staged 상태), 워킹 디렉터리의 파일 보존. 즉 모두 보존.
    –mixed : index 취소(add하기 전 상태, unstaged 상태), 워킹 디렉터리의 파일 보존 (기본 옵션)
    –hard : index 취소(add하기 전 상태, unstaged 상태), 워킹 디렉터리의 파일 삭제. 즉 모두 취소.

-   TIP 만약 워킹 디렉터리를 원격 저장소의 마지막 commit 상태로 되돌리고 싶으면, 아래의 명령어를 사용한다.
    단, 이 명령을 사용하면 원격 저장소에 있는 마지막 commit 이후의 워킹 디렉터리와 add했던 파일들이 모두 사라지므로 주의해야 한다.
    // 워킹 디렉터리를 원격 저장소의 마지막 commit 상태로 되돌린다.

```JavaScript
$ git reset --hard HEAD
```

### git push 취소하기

-   이 명령을 사용하면 자신의 local의 내용을 remote에 강제로 덮어쓰기를 하는 것이기 때문에 주의해야 한다.
    되돌아간 commit 이후의 모든 commit 정보가 사라지기 때문에 주의해야 한다.
    특히, 협업 프로젝트에서는 동기화 문제가 발생할 수 있으므로 팀원과 상의 후 진행하는 것이 좋다.

1. 워킹 디렉터리에서 commit 되돌린다.
    - 가장 최근의 commit을 취소하고 워킹 디렉터리를 되돌린다.

```JavaScript
// 가장 최근의 commit을 취소 (기본 옵션: --mixed)
$ git reset HEAD^
```

    - 원하는 시점으로 워킹 디렉터리를 되돌린다.

```JavaScript
// Reflog(브랜치와 HEAD가 지난 몇 달 동안에 가리켰었던 커밋) 목록 확인
$ git reflog 또는 $ git log -g
// 원하는 시점으로 워킹 디렉터리를 되돌린다.
$ git reset HEAD@{number} 또는 $ git reset [commit id]
```

2. 되돌려진 상태에서 다시 commit을 한다.

```JavaScript
$ git commit -m "Write commit messages"
```

3. 원격 저장소에 강제로 push 한다.

```JavaScript
$ git push origin [branch name] -f
또는
$ git push origin +[branch name]
```

```JavaScript
// Ex) master branch를 원격 저장소(origin)에 강제로 push
$ git push origin +master
```

TIP 경고를 무시하고 강제로 push 하기
[방법 1] -f 옵션
–force 옵션과 동일하다.
[방법 2] +[branch name]
해당 branch를 강제로 push한다.

### untracked 파일 삭제하기

-   git clean 명령은 추적 중이지 않은 파일만 지우는 게 기본 동작이다. 즉, .gitignore 에 명시하여 무시되는 파일은 지우지 않는다.

```JavaScript
$ git clean -f // 디렉터리를 제외한 파일들만 삭제
$ git clean -f -d // 디렉터리까지 삭제
$ git clean -f -d -x // 무시된 파일까지 삭제
```

TIP option
-d 옵션
디렉터리까지 지우는 것
-x 옵션
무시된 파일(.DS_Store나 .gitignore에 등록한 확장자 파일들)까지 모두 지우는 것
Ex) .o 파일 같은 빌드 파일까지도 지울 수 있다.
-n 옵션
가상으로 실행해보고 어떤 파일들이 지워질지 알려주는 것

```JavaScript
    git clean -n -d
    Would remove xxxx
    Would remove xx/

    git cloean -n -d -x
    Would remove xxxx
    Would remove xxx
    Would remove xx/
```
