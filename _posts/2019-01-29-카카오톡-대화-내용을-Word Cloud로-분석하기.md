---
layout: post
title: "카카오톡 대화 내용을 Word Cloud로 분석하기"
description: 
headline: 
modified: 2019-01-29
category: NLP
tags: [NLP, 카카오톡, Word Cloud, 대화 내용 분석]
imagefeature: 
mathjax: 
chart: 
share: true
comments: true
---

많은 사람이 카카오톡을 자주 사용한다. 그렇다면 사람들과 카카오톡을 한 내용에서 등장한 단어들을 한눈에 보여주는 `Word Cloud`를 작성하면 어떨까?

## 카카오톡 대화 내용 내보내기

![]({{ site.url }}/images/KakaoTalk_WC0.jpg)  
먼저 카카오톡 대화방 상단에 오른쪽 위를 클릭하고

![]({{ site.url }}/images/KakaoTalk_WC1.jpg)  
왼쪽 아래에 설정 창으로 이동한다.

![]({{ site.url }}/images/KakaoTalk_WC2.jpg)  
![]({{ site.url }}/images/KakaoTalk_WC3.jpg)  
대화 내용 내보내기를 클릭고 분석할 대화 내용의 텍스트를 내보낸다.

![]({{ site.url }}/images/KakaoTalk_WC4.jpg)  
![]({{ site.url }}/images/KakaoTalk_WC5.jpg)  
조금 기다리고 `python`을 사용할 수 있는 컴퓨터로 보낼 프로그램을 선택한다. 필자는 Gmail을 선택했다.

![]({{ site.url }}/images/KakaoTalk_WC6.jpg)  
보낸 후 다운로드를 받자.

## Word Cloud 제작
먼저 [Github Code](https://github.com/newhiwoong/Multipurpose_Word_Cloud)를 다운받자. 그리고 `Github`에 설치 부분을 따라 해서 `Word Cloud`를 제작할 수 있는 환경을 만들자.

![]({{ site.url }}/images/KakaoTalk_WC11.jpg)  
다운로드 받은 `KakaoTalkChats.txt`파일을 `Multipurpose_Word_Cloud`폴더 안에 넣자.

![]({{ site.url }}/images/KakaoTalk_WC7.jpg)  
`jupyter notebook`을 실행하고 필요한 라이브러리 import와 `keyword_count` 함수를 실행하자.

![]({{ site.url }}/images/KakaoTalk_WC8.jpg)  
`ls`명령어로 다운받은 파일이 잘 있는지 확인하고 `keyword_count`를 진행하자.

![]({{ site.url }}/images/KakaoTalk_WC9.jpg)  
`Word Cloud`를 진행하는데 필요한 함수들을 실행하고

![]({{ site.url }}/images/KakaoTalk_WC10.jpg)  
`make_cloud`를 실행해서 `Word Cloud`를 진행하자.

자신이 원하는 방식의 `Word Cloud` 제작을 위해서 아래 코드 설명을 참고하자.

```python
def make_cloud(tmp_data, back_image_n,state="no", font_n = "UnDinaru.ttf",background_color_n='white', max_font_size_n = 40):
back_image_n = "image 폴더에 있는 사진 중 Word Cloud의 모습이 되길 바라는 사진"
state = "Word Cloud의 표현되는 색"
       "no"         #랜덤하게 출력합니다.
       "grey"       #회색으로 출력합니다.
       "img"        #back_image_n 이미지의 색에 맞춰 출력합니다.
       (116,1,113)  #원하는 RGP로 표현합니다.
font_n = "Word Cloud에 적용할 폰트 이름"
background_color_n = "배경으로 바라는 색"
max_font_size_n = "Word Cloud에 표시할 글씨의 최대 크기"
```

## Word Cloud 예시

![]({{ site.url }}/images/KakaoTalk_WC1.png)  
![]({{ site.url }}/images/KakaoTalk_WC2.png)  
![]({{ site.url }}/images/KakaoTalk_WC3.png)  

이제 자신이 원하는 내용의 자기만의 `Word Cloud`를 만들어서 긴 대화 내용을 한눈에 알아보자.
