---
layout: post
title: 'Amazon Web Service'
description:
headline:
modified: 2021-12-20
category: Infrastructure
tags: [AWS]
mathjax:
chart:
share: true
comments: true
featured: true
disqus:
---

# Record


## 목차

-   [AWS Margate](#AWS-Margate)
-   [ECS](#ECS)
-   [EKS](#EKS)
-   [ECR](#ECR)
-   [EC2](#EC2)
-   [EFS](#EFS)
-   [S3](#S3)
-   [SES](#SES)
-   [SQS](#SQS)
-   [AWS Lambda](#AWS-Lambda)
-   [WAF](#WAF)
-   [CloudFront](#CloudFront)
-   [ELS](#ELS) 

## 개념

-

## 참조

-   AWS ( 아마존 웹서비스 ) 웹서버 만들기 [https://itadventure.tistory.com/372](https://itadventure.tistory.com/372)
    -   EC2 는 Elastic Compute Cloud(유연한 컴퓨팅 클라우드)
-   [AWS] Free-tier로 RDS 사용 중 요금을 지불했어요! [https://velog.io/@arara90/AWS-Free-tier%EB%A1%9C-RDS-%EC%82%AC%EC%9A%A9-%EC%A4%91-%EC%9A%94%EA%B8%88%EC%9D%84-%EC%A7%80%EB%B6%88%ED%96%88%EC%96%B4%EC%9A%94](https://velog.io/@arara90/AWS-Free-tier%EB%A1%9C-RDS-%EC%82%AC%EC%9A%A9-%EC%A4%91-%EC%9A%94%EA%B8%88%EC%9D%84-%EC%A7%80%EB%B6%88%ED%96%88%EC%96%B4%EC%9A%94)

## AWS Margate 
    - 컨테이너 제어 서버

## ECS
    - 컨테이너 배포, 관리

## EKS
    - ECS 에 kubernetes

## ECR
    - 이미지 관리

## EC2
    - 가상 컴퓨팅 환경

## EFS
    -파일 시스템

## S3
    - Simple Storage Service 객체 스토리지 서비스

## SES
    - Simple Email Service

## SQS
    - Simple Queue Service

## AWS Lambda
    - 서버리스 컴퓨팅 서비스

## WAF

## CloudFront

## ELS
    ### Application Load Balancer (ALB)
        - 계층: L7 (애플리케이션 계층)
        - 적합한 경우: HTTP/HTTPS 트래픽 라우팅
        - 기능:
            - URL, 호스트 헤더, path 등을 기반으로 트래픽 분산
            - 웹 트래픽에 대한 고급 라우팅 기능 제공 (스티키 세션, 호스팅된 콘텐츠 정적 캐싱, 컨텐츠 기반 라우팅 등)
            - 통합된 WAF (Web Application Firewall) 기능 제공

    ### Network Load Balancer (NLB)
        - 계층: L4 (트랜스포트 계층)
        - 적합한 경우: TCP/UDP 트래픽 라우팅
        - 기능:
            - IP 주소와 포트 번호를 기반으로 트래픽 분산
            - 간단하고 빠른 성능 제공
            - 낮은 비용