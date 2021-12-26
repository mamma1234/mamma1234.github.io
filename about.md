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

TypeScript, Visual Basic, C#, C++, JSP, CSS3, HTML5, Python, JavaScript, Java, ProC, goLang, Kotlin, <br>
Spring Boot, Spring, Spring Framework, AOP, Egovframework, MyBatis, Maven, <br>
Struts2, JSTL, Java Servlet,  <br>
React, jQuery, Bootstrap,  <br>
PostgreSQL, Mongo DB, MY-SQL, Oracle DB,  <br>
React-Native,  <br>
Elasticsearch, R, <br>
AWS, Docker, GCP, <br>
SVN, GitHub, CVS,  <br>
Linux, CentOS, Ubuntu <br>



<h2>Connect</h2>
✉️ [mamma1234@gmail.com](mailto:mamma1234@gmail.com)  
✉️ [mamma1234@naver.com](mailto:mamma1234@naver.com])  
🌐 [https://github.com/mamma1234](https://github.com/mamma1234)

<h2>My Stie</h2>
🌐 [Github https://github.com/mamma1234](https://github.com/mamma1234)
🌐 BLOG http://mamma1234.egloos.com/](http://mamma1234.egloos.com/)
🌐 [CAFE https://cafe.naver.com/mamma1234](https://cafe.naver.com/mamma1234)



## [EXPERIENCE]


### 화주통합서비스
- 기간
  - 2020년 ~ 현재
- 배경
  - 케이엘넷 새로운 사업 영역 확대를 위한 서비스 구축
- 서비스 설명
  - 해운선사 부킹, SR 통합 서비스
  - 선사스케쥴
  - 선박 해상 추적서비스
  - 컨테이너 추적 서비스
- 역할
  - 기획, 설계, 분석, 개발, PM
<figure>
	<img height="500px" width="500px" src="{{ site.url }}/images/plismplus.png" alt="portfolio">
	<figcaption> [booking.plism.com](https:.//booking.plism.com)</figcaption>
</figure>


### 위동부킹서비스
- 기간
  - 2021년 4월 ~ 2021년 8월
- 배경
  - 화주통합서비스 구축중 사업 범위내 위동선사에서 부킹 서비스 구축 의뢰하여 수행 
- 서비스 설명
  - 화주 부킹, SR 통합 서비스
  - 위동 선사, 컨펌, BL 수신 서비스
  - 위동 스케쥴, 부킹 Close, SR Close 서비스
  - 위동 선박 위치 서비스
- 역할
  - 기획, 설계, 분석, 개발, PM
<figure>
	<img height="500px" width="500px" src="{{ site.url }}/images/weidong.png" alt="portfolio">
	<figcaption> [weidong.plism.com](https:.//weidong.plism.com)</figcaption>
</figure>


### 솔루션연구팀
- 기간
  - 2016년 7월 ~ 2020년 12월
- 배경
  - PLISM 3.0 구축후 개발부서 (솔루션연구소) 서비스 운영 및 팀 관리 
-  설명
  - Etrans, Plism, LogisBill, Port-Mis, e-Logispis, EDI 중계, Xmapper등 시스템을 운영 및 유지보수, 관리
  - 솔루션 운영 기간중 역대 최소의 장애로 역대 가장 안정적 서비스를 제공하였으며
  - 역대 가장 많은 마이너 서비스 개발한 기간
- 역할
  - 팀장,파트장


### PLISM 3.0
- 기간
  - 2015년 7월 ~ 2016년 7월
- 배경
  - 케이엘넷의 영역 영역 공격적 확대를 위함, 경쟁업체와의 경쟁에서 우위를 점하고자 수행
  - 경쟁업체의 독점적 영역인 MFCS 취합시스템 진입
- 서비스 설명
  - 해상물류수입서비스 및 해양수산부, 관세청 통합 적하목록 신고 시스템
  - MFCS 선사, 포워더 적하목록 취합, 신고, 하선신고, 적하목록정정 시스템
  - 운송사, 포워더 등 수출입 주체 적하목록 수취 서비스
  - 수입 AN, C-DO, Invoice, 운송오더 시스템
  - 컨테이너 반출입 예약, 재고관리 시스템
  - 반입신고서, 적하일람표 해양수산부 신고 시스템
- 역할
  - 기획, 설계, 분석, 개발, PL
<figure>
	<img height="500px" width="500px" src="{{ site.url }}/images/plism.png" alt="portfolio">
	<figcaption> [www.plism.com](https:.//www.plism.com)</figcaption>
</figure>


### 케이엘넷 연구소
- 기간
  - 2013년 5월 ~ 2015년 6월
- 배경
  - 케이엘넷 내부 시스템 자동화 및 효율화를 수행
-  설명
  - ERP, CMS, 빌링 입금 자동화 시스템 - 경영 자동화, 효율화 지원 시스템 구축
  - 전자결재 - 전자 결재 전산 웹, 앱 시스템
  - 무증빙서비스 - 지출결재시 영수증 등 오프라인 증빙서류를 CMS, ERP 연동으로 자동 증빙 서비스 구축
  - PMS - 부서별 계획, 원가, 매출, 이익, 인력관리 시스템으로 의사결정 지원
- 역할
  - 기획, 설계, 분석, 개발, PM

### 복권시스템 안정화를 위한 병행운영 사업
- 기간
  - 2013년 1월 ~ 2013년 5월
- 배경
  - 기획재정부 복권시스템 국산화를 위한 사업
- 설명
  - LG CNS 협력업체로 사업 투입
  - 복권발급 운영 시스템 부분 담당
- 역할
  - 컨설턴트, 설계, TA

### 국토해양부 스마트포트 정보시스템 구축 사업
- 기간
  - 2012년 6월 ~ 2012년 12월
- 배경
  - 국토해양부 항만운영정보시스템과 3개항만청 항맘운영정보시스템과의 연동을 위함
- 설명
  - 국토해양부, 항만공사 항만운영정보시스템 통합을 위한 선행 사업
- 역할
  - PL, 설계, 개발

### 부산힝민공사 BPA-NET 구축 사업
- 기간
  - 2012년 3월 ~ 2012년 6월
- 배경
  - 부산항만공사 정보 시스템 신규 구축을 위한 사업
- 설명
  - 노후화된 부산항만공사 정보화 시스템을 신규로 구축하기 위한 사업
- 역할
  - PL, 설계, 개발

### 여수광양 항만운영정보시스템 신고검증체계 시스템 구축
- 기간
  - 2011년 12월 ~ 2012년 3월
- 배경
  - 여수광양 항만운영정보시스템 고도화 및 신고 정보의 정확도 이슈 해결을 위함
- 설명
  - 항만운영정보시스템 고도화
  - 신고 정보 검증을 위한 시스템 구축으로 정확도 해결을 위한 과제 수행
- 역할
  - PL, TA, 설계, 개발

### 인천항 항만물류 U-시스템 구축 3단계
- 기간
  - 2011년 6월 ~ 2011년 12월
- 배경
  - 인천항 항만운영정보시스템 (I-PLUS) 구축
- 설명
  - 항만운영정보 시스템 구축 년차
  - I-PLUS 구축 3개년 사업의 마지막 연도 구축 부문
- 역할
  - PL, 설계, 개발

### 부산항만공사 인센티브 검증시스템
- 기간
  - 2011년 4월 ~ 2011년 6월
- 배경
  - 부산지역 컨테이너 운송사 지원을 위한 인센티브 검증 시스템 구축
- 설명
  - 부산지역 터미널간 운송을 하는 운송사에 인센티브를 부여하기 위한 검증 시스템 구축
  - 운송사, 선사가 운송 내역을 상호 비교하여 검증하는 시스템
- 역할
  - PM, 설계

### 인천항 항만물류 U-시스템 구축 2단계
- 기간
  - 2010년 5월 ~ 2010년 12월
- 배경
  - 인천항 항만운영정보시스템 (I-PLUS) 구축
- 설명
  - 3단게 사업중 2단계 인천항 내부 시스템, ERP, 전자결재등 정보화 시스템 구축 년차
- 역할
  - TA, 컨설턴트

### 항해정기선사협의회 화물실적 통계 관리 시스템
- 기간
  - 2010년 3월 ~ 2010년 5월
- 배경
  - 항해 운송하는 선사의 화물 운송 실적 통계 관리하기 위한 시스템
- 설명
  - 서해, 중국간 화물을 정기적으로 운행하는 선사의 화물 실적을 통계내어 관리하기 위한 시스템
- 역할
  - PL, 개발

### 인천항 항만물류 U-시스템 구축 1단계
- 기간
  - 2009년 8월 ~ 2010년 3월
- 배경
  - 인천항 항만운영정보시스템 (I-PLUS) 구축
- 설명
  - 3단게 사업중 정보화 포탈 시스템 구축을 위한 원년도 사업
- 역할
  - TA, 설계

### 화물수송 최적화 시스템 구축 사업
- 기간
  - 2008년 10월 ~ 2009년 8월
- 배경
  - 철도청의 화물수송 정보화 사업
- 설명
  - 화물수송 예약제 시스템 구축을 위한 과제중 운송사와 철도청간의 중계 서비스 부분을 담당
- 역할
  - PL, 설계, 개발

### RFID-USN 기반 u-PORT 구축
- 기간
  - 2008년 4월 ~ 2009년 8월
- 배경
  - 해양수산부 주관 전국 수출입항 터미널 게이트에 RFID-USN 인프라 구축 사업
- 설명
  - 전국 터미널에 RFID 인프라룰 구축하여 USN 환경 시스템 구축하기 위함
  - 컨테이너에 RFID 433 Mhz tag를 부착
  - 차량에 900 Mhz tag를 부착
- 역할
  - RFID 미들웨어 컨설팅, 개발

### 케이엘넷 RFID 미들웨어 연구 개발
- 기간
  - 2006년 4월 ~ 2008년 4월
- 배경
  - 케이엘넷의 신성장 동력 RFID 연구를 위함
- 설명
  - 미래 신성장 동력인 RFID 미들웨어를 개발하여 시장을 주도하기 위함
- 역할
  - 미들웨어 개발 연구원

### 삼성전자 SCM (gSCM) 시스템 구축
- 기간
  - 2003년 10월 ~ 2006년 10월
- 배경
  - 삼성전자의 글로벌 SCM 체인 구축을 위함
- 설명
  - 사업부별, 국가별 별도 구축된 SCM 시스템을 하나의 gSCM으로 통합 구축
- 역할
  - 설계, 개발

### 포스코 CRM 시스템 구축
- 기간
  - 2002년 9월 ~ 2003년 9월
- 배경
  - 포스코 CRM 시스템 구축
- 설명
  - 오라클 글로벌 CRM 모듈을 포스코, 국내용으로 커스터마이징 사업
- 역할
  - 설계, 개발

### 비씨카드 구매카드시스템 구축
- 기간
  - 2000년 1월 ~ 2002년 7월
- 배경
  - 구매, 판매 기업간 어음,현금 대신 구매카드를 활용하여 신용거래가 가능하게 하기 위함
- 설명
  - 어음, 현금 대신 신용구매카드를 활용하여 혁신적 기업거래가 가능하게 됨
- 역할
  - 설계, 개발