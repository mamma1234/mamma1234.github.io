---
layout: page
permalink: /about/index.html
title: 박대규
tags: [mamma, mamma1234, parkdaekyu, dreamdae, pdkship]
imagefeature: fourseasons.jpg
chart: true
---

<figure>
	<img src="{{ site.url }}/images/mamma_2021-12-26 18.22.18.jpeg" alt="portfolio">
	<figcaption>portfolio</figcaption>
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

<!--
This is my personal blog. It currently has {{ site.posts | size }} posts in {{ site.categories | size }} categories which combinedly have {{ total_words }} words, which will take an average reader ({{ site.wpm }} WPM) approximately <span class="time">{{ total_readtime }}</span> minutes to read. {% if featuredcount != 0 %}There are <a href="{{ site.url }}/featured">{{ featuredcount }} featured posts</a>, you should definitely check those out.{% endif %} The most recent post is {% for post in site.posts limit:1 %}{% if post.description %}<a href="{{ site.url }}{{ post.url }}" title="{{ post.description }}">"{{ post.title }}"</a>{% else %}<a href="{{ site.url }}{{ post.url }}" title="{{ post.description }}" title="Read more about {{ post.title }}">"{{ post.title }}"</a>{% endif %}{% endfor %} which was published on {% for post in site.posts limit:1 %}{% assign modifiedtime = post.modified | date: "%Y%m%d" %}{% assign posttime = post.date | date: "%Y%m%d" %}<time datetime="{{ post.date | date_to_xmlschema }}" class="post-time">{{ post.date | date: "%d %b %Y" }}</time>{% if post.modified %}{% if modifiedtime != posttime %} and last modified on <time datetime="{{ post.modified | date: "%Y-%m-%d" }}" itemprop="dateModified">{{ post.modified | date: "%d %b %Y" }}</time>{% endif %}{% endif %}{% endfor %}. The last commit was on {{ site.time | date: "%A, %d %b %Y" }} at {{ site.time | date: "%I:%M %p" }} [UTC](http://en.wikipedia.org/wiki/Coordinated_Universal_Time "Temps Universel Coordonné").
-->

<h1 align="center">
<a href=""></a>  
</h1>

<figure>
  <img src="" alt="">
  <figcaption></figcaption>
</figure>

## [INTRODUCTION]()
XXXX

## [EXPERIENCE]()
### 관련사이트  - *링크*
- [Github https://github.com/mamma1234](https://github.com/mamma1234)
- [BLOG http://mamma1234.egloos.com/](http://mamma1234.egloos.com/)
- [CAFE https://cafe.naver.com/mamma1234](https://cafe.naver.com/mamma1234)


## [EDUCATION]()
### 경원대학교 - *전자계산학과*
<sub>94학번, 2002년 졸업</sub>  

## [Skills]()

### Language
Python, JavaScript, C

### Framework
Pandas, NumPy, scikit-learn, KoNLPy, Spark, [PyTorch](https://github.com/mamma1234/PyTorch), [TensorFlow](https://github.com/mamma1234/TensorFlow), [Keras](https://github.com/mamma1234/Keras-Applications)

### AI / ML
오일석의 '[패턴인식](http://www.yes24.com/24/goods/3315437?scode=032&OzSrank=1)', 마이클 네그네빗스키의 ‘[인공지능 개론](http://www.yes24.com/24/Goods/9386454?Acode=101)’ 독학으로 전통적인 ML 분야 학습, Vision + NLP + Sequence Models - [Coursera 강의](https://www.coursera.org/learn/nlp-sequence-models) 수료 및 각종 프로젝트 진행, [강화학습](https://event-us.kr/modu/event/2016) + [Deep Generative](https://event-us.kr/modu/event/4648) 스터디를 통하여 학습 및 실습


<h2>Connect</h2>
✉️ [mamma1234@gmail.com]()  
🌐 [https://github.com/mamma1234](https://github.com/mamma1234)


### XXXX - *Team project*
<sub>2018.10.07 - 12.20, [Github](https://github.com/mamma1234), [Report](https://bit.ly/mamma1234)</sub>
- 샘플 내용 1
- 샘플 내용 2

### XXXX - *Team project*
<sub>2018.10.07 - 12.20, [Github](https://github.com/mamma1234), [Report](https://bit.ly/mamma1234)</sub>
- 샘플 내용 1
- 샘플 내용 2