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
🌐 [BLOG http://mamma1234.egloos.com/](http://mamma1234.egloos.com/)  
🌐 [CAFE https://cafe.naver.com/mamma1234](https://cafe.naver.com/mamma1234)  



## [EXPERIENCE]
### 운송관리시스템
- 기간
  - 2022년 3월 ~ 현재
- 배경
  - 로지스팟 핵심 사업인 운송 관리 시스템의 안정화 및 지속적 성장 지원
  - AI 기반 최적화 기술 도입을 통한 경쟁력 강화
- 핵심 성과
  - 최적화 라우팅 신규 서비스 런칭으로 배송 효율 30% 향상, 연간 물류비 5억 원 절감 (예상)
  - 스크럼 및 맨투맨 관리로 프로젝트 일정 준수율 95% 달성
  - DevOps, Microservices 아키텍처 도입으로 배포 빈도 주 1회 → 일 3회 증가
- 서비스 설명
  - 운송사, 화주, 기사 도메인 통합 운영
  - 주문 → 최적화 → 배차 → 운행 → 정산 전 과정 자동화
  - 화주 ERP, WMS, OMS 등 외부 시스템 연동
  - 인성, 화물24시 등 화물망 유기적 통합
- 역할
  - PM, PO, TA, SA, DEV, OPS (다중 역할 수행)
- 대표 기술
  - PHP, Laravel,  Vue
  - Google OR-Tools, OSRM (라우팅 엔진 내재화)
  - AWS, GCP, Docker
  - Jenkins, Circle-CI, GitHub
  - Mysql, Rddis, Influx
  - JIRA, Slack
<figure>
	<img height="500px" width="500px" src="{{ site.url }}/images/client.png" alt="portfolio">
	<figcaption> [client.logi-spot.com](https://client.logi-spot.com)</figcaption>
  <img height="500px" width="500px" src="{{ site.url }}/images/carrier.png" alt="portfolio">
  <figcaption> [carrier.logi-spot.com](https://carrier.logi-spot.com)</figcaption>
</figure>

### 창고관리시스템
- 기간
  - 2022년 3월 ~ 2023년 3월
- 배경
  - 외부 솔루션 의존도 탈피 및 자사 물류 특성에 맞는 시스템 필요
  - 수기 관리 업무의 전산화를 통한 운영 효율 향상
- 핵심 성과
  - 외부 솔루션 → 자사 솔루션 전환으로 연간 라이선스 비용 3억 원 절감
  - 수기 업무 전산화 및 자동화로 운영 효율 200% 향상
  - 재고 정확도 95% → 99.8% 향상
  - 커스터마이징 대응 시간 평균 2주 → 3일 단축
- 서비스 설명
  - 입고, 출고, 재고, 수불, 정산, 마스터 관리
  - B2B, B2C 통합 운영
  - 보세, 식품, 의약품, 수입 상품 등 다양한 상품 유형 지원
  - 실시간 재고 추적 및 위치 관리
- 역할
  - PL, PO, DEV, TA
- 대표 기술
  - Spring Boot, MyBatis, Maven
  - Docker, Nginx
  - Oracle
  - JIRA, Slack
<figure>
	<img height="500px" width="500px" src="{{ site.url }}/images/wms.png" alt="portfolio">
	<figcaption> [wms.logi-spot.com](https://wms.logi-spot.com)</figcaption>
</figure>

### 화주통합서비스
- 기간
  - 2020년 1월 ~ 2022년 3월
- 배경
  - 케이엘넷 새로운 사업 영역 확대를 위한 서비스 구축
- 핵심 성과
  - 케이엘넷의 사업 다각화 및 지속 가능 성장 기반 마련
  - API 기반 플랫폼으로 외부 파트너사 연동 확대
- 서비스 설명
  - 국내 유일 해운선사 부킹, SR 통합 서비스
  - 국내 최대 선사스케쥴
  - 선박 해상 추적서비스
  - 국내 최정밀,실시간 컨테이너 추적 서비스
- 역할
  - 기획, 설계, 분석, 개발, PM
- 대표 기술
  - Python, React, Scrapy, Javascript
  - Docker, Nginx
  - 맞춤형 API 서버 구축
  - Jasper 기반 레포트 서버 구축
  - React-Native 앱 구축
  - Oauth2.0 통합 인증 서버 구축
  - Gcm Push 서버 구축중
  - Oracle, Postgresql, Mssql, ElasticSearcher
  - MiBatis, Maven, Spring Boot
<figure>
	<img height="500px" width="500px" src="{{ site.url }}/images/plismplus.png" alt="portfolio">
	<figcaption> [booking.plism.com](https:.//booking.plism.com)</figcaption>
</figure>


### 위동부킹서비스
- 기간
  - 2021년 4월 ~ 2021년 8월
- 배경
  - 화주통합서비스 구축중 사업 범위내 위동선사에서 부킹 서비스 구축 의뢰하여 수행 
- 핵심 성과
  - 선사 부팅 서비스 통합을 위한 기반 마련
- 서비스 설명
  - 화주 부킹, SR 통합 서비스
  - 위동 선사, 컨펌, BL 수신 서비스
  - 위동 스케쥴, 부킹 Close, SR Close 서비스
  - 위동 선박 위치 서비스
- 역할
  - 기획, 설계, 분석, 개발, PM
- 대표 기술
  - Python, React, Javascript
  - Docker, Nginx
  - Jasper 기반 레포트 서버 구축
  - Oauth2.0 통합 인증 서버 구축
  - Oracle, Postgresql
  - MiBatis, Maven, Spring Boot
<figure>
	<img height="500px" width="500px" src="{{ site.url }}/images/weidong.png" alt="portfolio">
	<figcaption> [weidong.plism.com](https:.//weidong.plism.com)</figcaption>
</figure>


### eBiz솔루션연구팀
- 기간
  - 2016년 7월 ~ 2020년 12월
- 배경
  - PLISM 3.0 구축후 개발부서 (솔루션연구소) 서비스 운영 및 팀 관리 
- 핵심 성과
  - 장애율 최소화 및 고객 만족도 최우수 달성
    - 테스트 자동화, 코드 리뷰로 품질 향상
    - 주기적 비상 대응 훈련, 상시 모니터링 체계 구축
  - 매출 최대 성장 기록
    - 단기 매출 100 억, 연간 매출 30 억 성장
  - 팀 관리 탁월성
    - 팀 사기 최고조 유지, 이전 이직률 50%를 5%이하로 낮추는 성과
  -  보안 및 품질 인증 획득
    - ISMS-P (정보보호 및 개인정보보호 관리체계) 인증 획득
-  설명
  - Etrans, Plism, LogisBill, Port-Mis, e-Logispis, EDI 중계, Xmapper등 시스템을 운영 및 유지보수, 관리
  - 솔루션 운영 기간중 역대 최소의 장애로 역대 가장 안정적 서비스를 제공하였으며
  - 역대 가장 많은 마이너 서비스 개발한 기간
- 역할
  - 팀장,파트장
- 대표 기술
  - Oracle
  - Java, Jquery, Javascript, ProC
  - ESB, Kafka
  - Jeus, EJB
  - Websquare, Miplatform, Gauce
  - Spring Framework, iBatis, Maven, Spring MVC, Spring Boot

### PLISM 3.0
- 기간
  - 2015년 7월 ~ 2016년 7월
- 배경
  - 케이엘넷의 영업 영역 공격적 확대를 위함, 경쟁업체와의 경쟁에서 우위를 점하고자 수행
  - 경쟁업체의 독점적 영역인 MFCS 취합 시장 진입
- 핵심 성과
  - 해상 분야 독점적 지위 확보
    - 해상 물류 시장점유율 0% 에서 95% 달성
    - 케이엘넷 매출 위기 국면에서 단기간 100억 원 이상 매출 성장 달성  
- 서비스 설명
  - 해상물류수입서비스 및 해양수산부, 관세청 통합 적하목록 신고 시스템
  - MFCS 선사, 포워더 적하목록 취합, 신고, 하선신고, 적하목록정정 시스템
  - 운송사, 포워더 등 수출입 주체 적하목록 수취 서비스
  - 수입 AN, C-DO, Invoice, 운송오더 시스템
  - 컨테이너 반출입 예약, 재고관리 시스템
  - 반입신고서, 적하일람표 해양수산부 신고 시스템
- 역할
  - 기획, 설계, 분석, 개발, PL
- 대표 기술
  - Oracle
  - Java, Jquery, Javascript, ProC
  - ESB, Kafka
  - Jeus, EJB
  - Websquare, Miplatform, Gauce
  - Spring Framework, iBatis, Maven, Spring MVC, Spring Boot
<figure>
	<img height="500px" width="500px" src="{{ site.url }}/images/plism.png" alt="portfolio">
	<figcaption> [www.plism.com](https:.//www.plism.com)</figcaption>
</figure>


### 케이엘넷 연구소
- 기간
  - 2013년 5월 ~ 2015년 6월
- 배경
  - 케이엘넷 내부 시스템 자동화 및 효율화 목표
  - 케이엘넷 신규 사업 운송 관리 시스템 구축
- 핵심 성과
  - 경영 프로세스 자동화 및 운영 비용 절감
    - 엑셀 등 수작업 프로세스 80% 자동화
    - 인건비 및 운영비 연간 2 m/m 절감
    - 법인 카드 영수증 첨부 자동화
    - 프로젝트, 코스트센터별 매출,매입 장부 관리 자동화
  - 신규 사업 영역 확대
    - TMS 운송 관리 분야 진출 기반 마련
- 설명
  - ERP, CMS - 회계 전산화 시스템 구축
  - 빌링 입금 자동화 시스템 - 경영 자동화, 효율화 지원 시스템 구축
  - 전자결재 - 전자 결재 전산 웹, 앱 시스템 구축
  - 무증빙서비스 - 지출결재시 영수증 등 오프라인 증빙서류를 CMS, ERP 연동으로 자동 증빙 서비스 구축
  - PMS - 부서별 계획, 원가, 매출, 이익, 인력관리 전산화로 의사결정 지원 시스템 구축
  - 이트럭뱅크 - 케이엘넷의 새로운 사업 분야, 운송관리시스템 TMS 프레임워크 개발
- 역할
  - 기획, 설계, 분석, 개발, PM
- 대표 기술
  - Oracle, Mssql
  - Java, Jquery, Javascript
  - Tomcat, Apache
  - Spring Framework, iBatis, Maven, Spring MVC

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
- 대표 기술
  - Oracle
  - Java, Jsp, Servlet
  - Spring Framework, iBatis, Maven, Spring MVC

### 국토해양부 스마트포트 정보시스템 구축 사업
- 기간
  - 2012년 6월 ~ 2012년 12월
- 배경
  - 국토해양부 항만운영정보시스템과 3개항만청 항맘운영정보시스템과의 연동을 위함
- 설명
  - 국토해양부, 항만공사 항만운영정보시스템 통합을 위한 선행 사업
- 역할
  - PL, 설계, 개발
- 대표 기술
  - Oracle
  - Java, Jsp, Servlet
  - Websquare
  - Spring Framework, iBatis, Maven, Spring MVC

### 부산항만공사 BPA-NET 구축 사업
- 기간
  - 2012년 3월 ~ 2012년 6월
- 배경
  - 부산항만공사 정보 시스템 신규 구축을 위한 사업
- 설명
  - 노후화된 부산항만공사 정보화 시스템을 현대화하기 위한 사업
- 역할
  - PL, 설계, 개발
- 대표 기술
  - Oracle
  - Java, Jsp, Servlet
  - Websquare
  - Spring Framework, iBatis, Maven, Spring MVC

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
- 대표 기술
  - Oracle
  - Java, Jsp, Servlet
  - Miplatform
  - Spring Framework, iBatis, Maven, Spring MVC

### 인천항 항만물류 U-시스템 구축 3단계
- 기간
  - 2011년 6월 ~ 2011년 12월
- 배경
  - 인천항 항만운영정보시스템 (I-PLUS) 구축
- 설명
  - 항만운영정보 시스템 구축
  - I-PLUS 구축 3개년 사업의 마지막 연도 구축 부문
- 역할
  - PL, 설계, 개발
- 대표 기술
  - Oracle
  - Java, Jsp, Servlet
  - Miplatform
  - Spring Framework, iBatis, Maven, Spring MVC

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
- 대표 기술
  - Oracle
  - Java, Jsp, Servlet
  - Spring Framework, iBatis, Maven, Spring MVC

### 인천항 항만물류 U-시스템 구축 2단계
- 기간
  - 2010년 5월 ~ 2010년 12월
- 배경
  - 인천항 항만운영정보시스템 (I-PLUS) 구축
- 설명
  - 3단게 사업중 2단계 인천항 내부 시스템, ERP, 전자결재등 정보화 시스템 구축 년차
- 역할
  - TA, 컨설턴트
- 대표 기술
  - Oracle
  - Java, Jsp, Servlet
  - Miplatform
  - Spring Framework, iBatis, Maven, Spring MVC

### 항해정기선사협의회 화물실적 통계 관리 시스템
- 기간
  - 2010년 3월 ~ 2010년 5월
- 배경
  - 항해 운송하는 선사의 화물 운송 실적 통계 관리하기 위한 시스템
- 설명
  - 서해, 중국간 화물을 정기적으로 운행하는 선사의 화물 실적을 통계내어 관리하기 위한 시스템
- 역할
  - PL, 개발
- 대표 기술
  - Oracle
  - Java, Jsp, Servlet
  - Spring Framework, iBatis, Maven, Spring MVC

### 인천항 항만물류 U-시스템 구축 1단계
- 기간
  - 2009년 8월 ~ 2010년 3월
- 배경
  - 인천항 항만운영정보시스템 (I-PLUS) 구축
- 설명
  - 3단게 사업중 정보화 포탈 시스템 구축을 위한 원년도 사업
  - 포탈 구축 담당 수행
- 역할
  - TA, 설계
- 대표 기술
  - Oracle
  - Java, Jsp, Servlet
  - Miplatform
  - Spring Framework, iBatis, Maven, Spring MVC

### 화물수송 최적화 시스템 구축 사업
- 기간
  - 2008년 10월 ~ 2009년 8월
- 배경
  - 철도청의 화물수송 정보화 사업
- 설명
  - 화물수송 예약제 시스템 구축을 위한 과제중 운송사와 철도청간의 중계 서비스 부분을 담당
- 역할
  - PL, 설계, 개발
- 대표 기술
  - Oracle
  - Java, Jsp, Servlet
  - Spring Framework, iBatis, Maven, Spring MVC

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
- 대표 기술
  - Oracle
  - Java, Jsp, Servlet
  - Jquery

### 케이엘넷 RFID 미들웨어 연구 개발
- 기간
  - 2006년 4월 ~ 2008년 4월
- 배경
  - 케이엘넷의 신성장 동력 RFID 연구를 위함
- 설명
  - 미래 신성장 동력인 RFID 미들웨어를 개발하여 시장을 주도하기 위함
- 역할
  - 미들웨어 개발 연구원
- 대표 기술
  - Java, Jsp, Servlet
  - Jquery

### 삼성전자 SCM (gSCM) 시스템 구축
- 기간
  - 2003년 10월 ~ 2006년 10월
- 배경
  - 삼성전자의 글로벌 SCM 체인 구축을 위함
- 설명
  - 사업부별, 국가별 별도 구축된 SCM 시스템을 하나의 gSCM으로 통합 구축
- 역할
  - 설계, 개발
- 대표 기술
  - Jeus
  - Oracle
  - Java, Jsp, Servlet
  - Miplatform, Gauce
  
### 포스코 CRM 시스템 구축
- 기간
  - 2002년 9월 ~ 2003년 9월
- 배경
  - 포스코 CRM 시스템 구축
- 설명
  - 오라클 글로벌 CRM 모듈을 포스코, 국내용으로 커스터마이징 사업
- 역할
  - 설계, 개발
- 대표 기술
  - Oracle
  - Java, Jsp, Servlet
  

### 비씨카드 구매카드시스템 구축
- 기간
  - 2000년 1월 ~ 2002년 7월
- 배경
  - 구매, 판매 기업간 어음,현금 대신 구매카드를 활용하여 신용거래가 가능하게 하기 위함
- 설명
  - 어음, 현금 대신 신용구매카드를 활용하여 혁신적 기업거래가 가능하게 됨
- 역할
  - 설계, 개발
- 대표 기술
  - Tuxedo, Weblogic
  - Oracle
  - Java, Jsp, Servlet, ProC, Visual Basic