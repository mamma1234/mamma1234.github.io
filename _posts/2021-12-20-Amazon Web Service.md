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
-   [ACL](#ACL) 
-   [ELB](#ELB) 
-   [EBS](#EBS) 

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

## ACL
    AWS ACL(Access Control List)은 네트워크 리소스에 대한 액세스 제어를 관리하는 데 사용되는 기능

## ELB
    ELB는 Elastic Load Balancing의 약자로, AWS에서 제공하는 관리형 로드 밸런서 서비스입니다. ELB는 여러 EC2 인스턴스나 컨테이너 등의 백엔드 리소스에 들어오는 트래픽을 분산하여 각 리소스에 대한 부하를 균등하게 분산시키는 역할을 합니다.
    ALB, NLB, GLB

## EBS
### 볼륨 크기 조정 후 파일 시스템 확장
    https://docs.aws.amazon.com/ko_kr/ebs/latest/userguide/recognize-expanded-volume-linux.html
    Xen 계열
        sudo lsblk
        sudo growpart /dev/xvda 1
        sudo lsblk
        sudo resize2fs /dev/root