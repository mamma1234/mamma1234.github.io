---
layout: post
title: "Disqus로 Github 블로그 댓글 기능 추가"
description: 
headline: 
modified: 2019-01-27
category: webdevelopment
tags: [blog, github, jekyll]
imagefeature: 
mathjax: 
chart: 
share: true
comments: true
---

독자와의 소통을 위해서는 블로그에 댓글을 쓸 수 있는 기능이 필요하다. [Disqus](https://disqus.com/)를 이용해서 블로그에 댓글 기능을 추가할 것이다.

먼저 [disqus 로그인](https://disqus.com/profile/login/) 혹은 회원가입을 하자, 만약 Google 계정 등이 있다면 더 간단하게 회원가입을 할 수 있다.

![]({{ site.url }}/images/blog17.JPG)  

그리고 왼쪽 위에서 Setting에 들어가 필요한 정보들을 기재한다.

![]({{ site.url }}/images/blog18.JPG)  
![]({{ site.url }}/images/blog19.JPG)  

그리고 다시 [Disqus 사이트](https://disqus.com/)로 들어와서 GET STARTED를 클릭하고

![]({{ site.url }}/images/blog20.JPG)  

`I want to install Disqus on my site` 버튼을 클릭하여 댓글 기능 추가를 시작한다.

![]({{ site.url }}/images/blog21.JPG)  

그리고 Website Name, Category를 지정하고 `Create Site`를 클릭한다.

![]({{ site.url }}/images/blog22.JPG)  

나는 돈이 없기에 Basic 즉 공짜인 것을 선택했다. 돈이 있다면 다른 기능으로 사는 것도 좋을 거 같다.

![]({{ site.url }}/images/blog23.JPG)  

이 사이트는 `Jekyll` 기반의 사이트이므로 `Jekyll`을 선택한다.

![]({{ site.url }}/images/blog24.JPG)  

그리고 스크롤을 조금 내려서 `Universal Embed Code`를 누르고 

![]({{ site.url }}/images/blog25.JPG)  

모든 내용을 복사해서 `ctrl + a` + `ctrl + c` `_includes` 폴더에 `disqus_comments.html` 파일에 붙여넣기 `ctrl + v`를 하고 

![]({{ site.url }}/images/blog26.JPG)  
![]({{ site.url }}/images/blog27.JPG)  

`git pull`을 진행하면 아래와 같이 댓글을 쓸 수 있다.

![]({{ site.url }}/images/blog28.JPG)  