---
layout: page
permalink: /about/index.html
title: 꿈을 간직한 이, 박대규
tags: [mamma, mamma1234, parkdaekyu, dreamdae, pdkship]
imagefeature: fourseasons.jpg
chart: true
---

<figure>
	<img src="{{ site.url }}/images/mamma_2021-12-26.jpeg" alt="portfolio">
	<figcaption>2021년 8월 6일 금요일 오후 5:52</figcaption>
</figure>

{% assign total_words = 0 %}
{% assign total_readtime = 0 %}
{% assign featuredcount = 0 %}
{% assign statuscount = 0 %}

{% for post in site.posts %}
    {% assign post_words = post.content | strip_html | number_of_words %}
    {% assign readtime = post_words | append: '.0' | divided_by:200 %}
    {% assign total_words = total_words | plus: post_words %}
    {% assign total_readtime = total_readtime | plus: readtime %}
    {% if post.featured %}
    {% assign featuredcount = featuredcount | plus: 1 %}
    {% endif %}
{% endfor %}

## [INTRODUCTION]
안녕하세요. 오래된 개발자 하지만 기술 만큼은 최신을 추구하는 개발자 입니다.


## [EDUCATION]
### 경원대학교 - *전자계산학과*  >> 가천대학교 대학교 이름 변경
<sub>94학번, 2002년 졸업</sub>  

### certificate
- 2001.06	자격증/면허증	정보처리기사	한국산업인력공단	최종합격
- 2019.11	자격증/면허증	초경량비행장치 조종자	한국교통안전공단	최종합격
- 현재 부동산중개사 시험 도전중



## [Skills]
<pre><code>
Struts2, Spring Framework, TypeScript, Java Servlet, JSP,
Visual Basic, SVN, GitHub, PostgreSQL, Mongo DB, MY-SQL,
Oracle DB, C#, C++, Bootstrap, Spring Boot, Spring, 
React, CSS3, HTML5, jQuery, Python, JavaScript, Java, 
goLang, React-Native, ProC, Egovframework, MyBatis, R,
Elasticsearch, Kotlin
</code></pre>


<h2>Connect</h2>
✉️ [mamma1234@gmail.com](mamma1234@gmail.com)  
✉️ [mamma1234@naver.com](mamma1234@naver.com])  
🌐 [https://github.com/mamma1234](https://github.com/mamma1234)



## [EXPERIENCE]
### EXPERIENCE


### XXXX - *Team project*
<sub>2018.10.07 - 12.20, [Github](https://github.com/mamma1234), [Report](https://bit.ly/mamma1234)</sub>
- 샘플 내용 1
- 샘플 내용 2

### XXXX - *Team project*
<sub>2018.10.07 - 12.20, [Github](https://github.com/mamma1234), [Report](https://bit.ly/mamma1234)</sub>
- 샘플 내용 1
- 샘플 내용 2




### 관련사이트  - *링크*
- [Github https://github.com/mamma1234](https://github.com/mamma1234)
- [BLOG http://mamma1234.egloos.com/](http://mamma1234.egloos.com/)
- [CAFE https://cafe.naver.com/mamma1234](https://cafe.naver.com/mamma1234)
