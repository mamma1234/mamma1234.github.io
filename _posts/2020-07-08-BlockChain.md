---
layout: post
title: "BlockChain"
description: 
headline: 
modified: 2020-07-08
category: webdevelopment
imagefeature: cover3.jpg
tags: [BlockChain]
mathjax: 
chart: 
share: true
comments: true
featured: true
disqus:
---

## Hyperledger
- 리눅스 재단에서 주관하는 블록체인 오픈소스 프로젝트

## Hyperledger 장점
- private
- golang, Node.js
- 병렬처리
- 허가 받은 사람만 장부(ledger) 공개
- 교체 가능한 합의 프로토콜 (SOLO, Kafka, PBFT 등)
- 문제 발생시 책임 소재가 분명
- 여러 산업에 범용적으로 도입 가능한 기술 표준 제시

- 속도가 빠름
- 보안성인 우수

- Configurable Module 구조: 조립식
- 일반 개발 언어 사용 가능
- 

## Hyperledger 구성
Asset, Chaincode, Ledger, Privacy, Security & Membershp Service, Consensus

Asset : 네트워크내 거래 대상, state 변화 - ledger 기록
Ledger : State 값의 변하는 것을 한줄한줄 기록해 둔 것 [ = blockchain] 
Chaincode : state 값에 변화를 주고 ledger에 업데이트를 하는 실제 로직 부분 [ = smart contract ]
Consensus : 합의, 블록체인 네트워크 내 peer 들이 항상 동기화된 State과 원장을 갖도록 하는 기술 [ = transaction ]
    - endorsement policy (보증)
    - Ordering service
Privacy : 서브넷(채널) 
Security & Membershp Service : Membership Service Provider, endorser (양도자), orderer (주문자)

### 하이퍼레저 프레임워크 (Hyperledger Framework)
하이퍼레저 패브릭 (Hyperledger Fabric)
    - Consensus, Membership service 등 Plug-and-Play 방식 구현
하이퍼레저 소투스 (Hyperledger Sawtooth)
    - 분산 원장 구축, 디플로이, 실행을 위한 모듈러 플랫폼
    - Proof of Elapsed Time (PoET) Consensus 알고리즘
    - 중앙세서 관리되지 않는 asset ownership... 디지털 레코드
하이퍼레저 이로하 (Hyperledger Iroha)
    - 모바일 어플리케이션 개발에 초점을 둔 분산 원장 개발 프로젝트
    - Byzantine Falut Tolerant 컨센서스 알고리즘
하이퍼레저 인디 (Hyperledger Indy)
    - 인증에 특화된 프로젝트
    - 블록체인에 기반한 독립적인 디지털 아이텐티티 레코드 생성
하이퍼레저 버로우 (Hyperledger Burrow)
    - Ethereum Virtual Machine (EVM) 에 기반한 스마트 컨트랙트 인터프리터가 빌트인된 블록체인 클라이언트를 제공
하이퍼레저 베수 (Hyperledger Besu)
하이퍼레저 그리드 (Hyperledger Grid)


### 하이퍼레저 툴 (Hyperledger Tool)
하이퍼레저 캘리퍼 (Hyperledger Caliper)
하이퍼레저 첼로 (Hyperledger Cello)
    - as-a-service 디플로이 모델이 가능하게 해줌
    - 블록체인 네트워크 생성, 관리, 삭제 소요되는 노력 최소화
하이퍼레저 익스플로러 (Hyperledger Explorer)
    - 원장에 담긴 정보를 쉽고 빠르게 조회하도록 하는 툴
하이퍼레저 캑터스 (Hyperledger Cactus)
하이퍼레저 아발론 (Hyperledger Avalon)
하이퍼레저 퀼트 (Hyperledger Quilt)
    - ILP 라는 결재 프로토콜로 원장 시스템간 interoperate를 가능하게 해줌
    - 분산 원장과 일반 원장간의 값 전송이 가능하게 해줌
하이퍼레저 우르사 (Hyperledger URSA)
하이퍼레저 에리즈 (Hyperledger Aries)
하이퍼레저 트랜잭트 (Hyperledger Transact)
하이퍼레저 컴포저 (Hyperledger Composer)
    - 블록체인 비즈니스 네트워크 구축
    - 스마트 컨트랙트 및 원간장에 그 컨트랙트가 돌아가도록 함
    - 전체적인 틀을 잡아준다고 생각하면 된다고...



#### 하이퍼레져 패브릭 네트워크
오더링 서비스 (O)
생성된 네트워크에 대한 정책 (NP)
클라이언트 어플리케이션 (CA)
어플리케이션을 소유하는 네트워크 참가조직 (RD)
네트워크내 컴포넌트 간의 프라이빗한 통신을 지원하는 커뮤니테이션 도구 채널 (C1)
채널의 정책 (CP) - Channel Policy

- Endorsing Peer: 스마트 컨트랙트에 수행될 트랜잭션을 시뮬레이션 해보고 그 결과를 클라이언트 어플리케이션에 리턴해주는 피어, 트랜잭션을 검증하는 역할
- Committing Peer: 오더링까지 되어서 전달된 트랜잭션 블럭을 검증하고, 검증이 완료되면 자기가 갖고 있는 원장에 해당 블럭을 추가하고 관리, 모든 피어는 기본적으로 committing peer
- Anchor peer: 채널내의 대표 피어, 채널에 다른 조직이 가입하면 가장 먼저 발견하는 피어
- Leading Peer: 모든 피어를 대표하여 네트워크와 커뮤니케이션하는 피어

#### 하이퍼레져 패브릭 트랜잭션
- Execute-Order-Validate
- 다른 플랫폼은 Execute-Validate

transaction proposal (요청)
    endorsement policy (거래 승인, 검증, 전송)
Endorsing peers 서명 확인, 트랜잭션 실행
Proposal responses 검토
클라이언트가 Transaction 전달
Committing Peer 에서 트랜잭션을 검증하고 커밋
Ledger updated

#### 하이퍼레져 패브릭 트랜잭션 gRPC

#### 하이퍼레져 패브릭 합의 알고리즘