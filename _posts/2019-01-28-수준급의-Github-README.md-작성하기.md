---
layout: post
title: "수준급의 Github README.md 작성하기"
description: 
headline: 
modified: 2019-01-28
category: 기타 정보 공유
tags: [README.md, github, Emoji, shields]
imagefeature: 
mathjax: 
chart: 
share: true
comments: true
---

Github README.md를 예쁘게 만들고 싶을 것이다. 오늘은 [shields](https://shields.io/#/)와 [Eemoji](https://missive.github.io/emoji-mart/) 그리고 [LICENSE](https://www.olis.or.kr/images/egovframework/olisImage/common/OpensourceSW_License_Guide.pdf)를 이용해서 수준급의 README.md를 작성하는 방법을 알아볼 것이다.



![]({{ site.url }}/images/readme1.JPG)  

내가 만든 예쁜 [README.md](https://github.com/newhiwoong/National-Petition) 예시



### Eemoji

Eemoji는 우리가 잘 아는 이모티콘을 의미한다. 예로  👜🕶👑🍁🎖🎨이러한 모든 것들이 Eemoji이다. README.md에서 적절한 부분에 Eemoji를 붙이면 훨씬 예쁜 ⭐README.md⭐ 파일을 작성할 수 있다.



#### Eemoji 사이트

- [emoji.muan](https://emoji.muan.co/#star) Eemoji를 검색할 수 있고 가장 정리가 잘 된 사이트.

- [Emoji Mart](https://missive.github.io/emoji-mart/) GIthub Edit status와 같이 이모지 검색이 가능한 사이트

- [emoji markup](https://gist.github.com/rxaviers/7360908) 여러 Eemoji들이 정리된 사이트



![]({{ site.url }}/images/readme2.JPG)  

[emoji.muan](https://emoji.muan.co/#star)에서 star를 검색한 예시



위 사이트를 이용해서 Eemoji들을 찾아서 이용해보자.



### Shields

shields는 무엇일까? 아래와 같이 자신의 Github를 소개하는 뱃지  정도라고 생각하면 될 것이다. license, web, version 등을 표시할 수 있다.

[![Stargazers](https://img.shields.io/badge/National--Petition-Stargazers-yellow.svg)](https://github.com/newhiwoong/National-Petition/stargazers)
[![license](https://img.shields.io/badge/license-Apache%202.0-red.svg)](https://www.apache.org/licenses/LICENSE-2.0)
[![results](https://img.shields.io/badge/results-Report-blue.svg)](https://paper.dropbox.com/doc/National-Petition-Analysis--AWBChEBfGCjv1j~TH2oJMUKbAg-RYdzoQNc8lAHVcDucJu1K)
[![data](https://img.shields.io/badge/data-web-brightgreen.svg)](https://www1.president.go.kr/petitions)



#### 사용법

[shields.io](https://shields.io/#/)에서 SUBJECT(제목), STATUS(상태), COLOR(색깔)를 지정하면 shields를 제작할 수 있다.  



![]({{ site.url }}/images/readme3.JPG)  

![](https://img.shields.io/badge/shields-go-green.svg)  



`https://img.shields.io/badge/<SUBJECT>-<STATUS>-<COLOR>.svg` 또는 여기서 직접 사용해도 될다.  

`https://img.shields.io/badge/shields-go-green.svg` 위 shieds를 만드는 링크이다.



이제 이러한 방법들을 응응해서 더욱 예쁜 README.md 파일을 만들기 바란다.



### LICENSE

LICENSE는 그냥 말 그대로 이 프로그램을 어디까지 사용해도 되는지 설명하는 것을 의미한다. [오픈소스 소프트웨어 라이선스 가이드 3.0](https://www.olis.or.kr/images/egovframework/olisImage/common/OpensourceSW_License_Guide.pdf) 문서를 읽고 원하는 LICENSE를 선택하고 Github에 적용해보자.



![]({{ site.url }}/images/readme4.JPG)  

프로젝트의 `Insights`에 들어가서



![]({{ site.url }}/images/readme5.JPG)  

`Cimmunity`에 들어가서 `License` 부분에 `Add`를  클릭한다.



![]({{ site.url }}/images/readme6.JPG)  

여기서 자신이 원하는 LICENSE를 선택하고 `Review and submit`을 눌러서 적용한다.



![]({{ site.url }}/images/readme7.JPG)  

![]({{ site.url }}/images/readme8.JPG)  

![]({{ site.url }}/images/readme9.JPG)  

따라 하고 `Merge pull request`를 누르면



![]({{ site.url }}/images/readme10.JPG)  

위 사진처럼 `License`가 적용돼 있다.



![]({{ site.url }}/images/readme11.JPG)

그리고 항상 Github에 업데이트한 내용이 있으면 `git pull`를 하는 것을 기억하자.



`git pull origin master`



## 더 많은 정보

그리고 더 많은 정보를  알고 싶으면 [README.md 템플릿](https://github.com/sujinleeme/readme-template/tree/master/korean) 을 참고 해서 자시만의 먼지 README.md파일을 만들기 바란다.


