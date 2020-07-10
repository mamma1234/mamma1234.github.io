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

## Hyperledger Fabric 용어
- Transactor : 트랜잭션(거래)을 일으키는 엔티티를 말합니다. 대표적으로 클라이언트 애플리케이션이 됩니다.
- Transaction : 트랜잭션은 블럭체인 네트워크에 대해서 비즈니스 로직을 수행하기 위한 요청입니다. 트랜잭션의 유형은 deploy, invoke 및 query 이며, 체인코드를 통해서 사전 정의된 인터페이스에 대한 함수를 구현합니다.
- Ledger : 트랜잭션과 현재 세계 상태를 포함하는 일련의 암호 학적으로 링크 된 블록. 이전 거래의 데이터 외에도 원장에는 현재 실행중인 체인 코드 애플리케이션의 데이터가 포함되어 있습니다.
- World state : 트랜잭션에 의해서 체인코드가 호출될 때 상태 및 데이터 저장을 위한 Key-value 데이터베이스 입니다.
- Chaincode : 다양한 트랜잭션의 유형을 구현한 블록체인에 임베드되는 로직입니다. 개발자에 의해 체인코드가 작성되고 블록체인 네트워크로 디플로이 합니다. 최종 사용자는 블록체인 네트워크를 구성하는 피어 또는 노드와 인터페이스 되어 있는 클라이언트 애플리케이션을 통해서 체인코드를 실행시킵니다. 체인코드는 트랜잭션을 일으키고 유효성이 확인되면 공유원장에 추가하고 World state를 수정합니다.
- Validating peer (VP) : 블록체인 네트워크에서 원장을 관리 유지하기 위해서 트랜잭션의 유효성을 검증하는 합의 프로토콜을 실행하는 노드입니다. 검증된 트랜잭션은 원장에 블록 단위로 추가됩니다. 트랜잭션이 합의에 실패하면 블록에서 제거되므로 장부에 기록되지 않습니다. Validating peer는 체인코드를 deploy, invoke, query 할 권한을 가집니다.
- Non-validating peer (NVP) : Transactor가 Validating peer에 접속 할 수 있도록 프록시 역할을 하는 노드입니다. Non-validating peer (NVP) 는 호출된 요청을 Validating peer로 전달하며, 이벤트 스트림, REST 서비스를 담당하는 노드입니다.
- Consensus : 블록체인 네트워크의 트랜잭션(deploy, invoke) 순서를 유지하는 프로토콜, Validating 노드들은 합의 프로토콜을 구현하여 트랜잭션을 승인하기 위해서 함께 동작합니다.
- Permissioned network : 각 노드는 블록체인 네트워크에서 접근 권한을 관리해야 하는 노드이며, 각 노드는 권한이 있는 사용자만 접근할 수 있습니다.


## Services
- Membership Services
멤버십 서비스는 블록체인 네트워크에서 인증 서비스를 제공합니다. Non-permissioned 블록체인의 경우 사용자 인증이 필요없으며, 모든 노드는 동등하게 트랜잭션 처리가 가능하고 블록에 트랜잭션 정보를 입력할 수 있습니다. 멤버쉽 서비스는 PKI(Public Key Infrastructure)와 분산화/합의 컴포넌트를 non-permissioned 블록체인에서 permissioned 블록체인으로 변환시킵니다. Permissioned 블록체인에서는 엔티티가 장기적인 인증서(enrollment certificates)를 획득하기 위해 등록절차를 거치게 되며, 엔티티 유형에 따라 구별될 수 있습니다. 사용자의 경우 TCA (Transaction Certificate Authority)가 인증서를 발급 할 수 있습니다. 여기서 획득한 인증서는 트랜잭션을 발생시킬때 인증하는데 사용됩니다.

- Blockchain Services
블록체인 서비스는 HTTP/2 표준을 기반으로 P2P 프로토콜을 통해서 분산원장을 관리합니다. 데이터 구조는 해시 알고리즘을 통해 World state를 복제하는 등 관리 하는데 가장 효율적으로 관리할 수 있도록 최적화되어 있습니다. 필요에 따라 다른 합의 알고리즘 플러그인(PBFT, Raft, PoW, PoS)을 연결하고 구성 할 수 있습니다.

- Chaincode Services
체인코드 서비스는 Validating 노드에서 안전하고 가벼운 방법으로 체인코드가 실행되도록 보장합니다. 환경은 보안 OS 및 체인 코드 언어, Go, Java 및 Node.js의 런타임 및 SDK 계층을 포함하는 일련의 서명 된 기본 이미지와 함께 “잠긴”보안 컨테이너입니다. 필요한 경우 다른 언어를 사용할 수 있습니다.

- Events
Validating peers 와 체인코드는 블록체인 네트워크에서 이벤트를 발생 할 수 있습니다. 이벤트 발생을 대기하고 있는 애플리케이션에 필요한 노티를 보냅니다. 이벤트는 미리 정의된 이벤트 혹은 커스텀 이벤트를 발생 할 수 있으며, 하나 이상의 어댑터를 통해 이벤트 수신 할 수 있습니다. 또한 Web hooks나 Kafka 등을 이용하여 이벤트 수신도 가능합니다.

- Application Programming Interface (API)
Fabric에 대한 기본 인터페이스는 REST API 입니다. API 호출을 통해 사용자 등록, 블록체인에 대한 쿼리, 트랜잭션 발생 들을 할 수 있습니다. 특히 체인코드와 상호작용하기 위한 API를 통해서 트랜잭션을 관리 할 수 있습니다.

- Command Line Interface (CLI)
REST API의 일부 기능을 지원하는 CLI기능을 통해서 체인코드의 디플로이 및 트랜잭션 처리 등을 빠르게 진행할 수 있도록 합니다. CLI는 Golang으로 제작이 되었으며 다양한 OS를 지원합





### 하이퍼레저 프레임워크 (Hyperledger Framework)
하이퍼레저 패브릭 (Hyperledger Fabric)
    - Consensus, Membership service 등 Plug-and-Play 방식 구현
하이퍼레저 소투스 (Hyperledger Sawtooth)
    - 분산 원장 구축, 디플로이, 실행을 위한 모듈러 플랫폼
    - 복권 설계 합의 프로토콜 Proof of Elapsed Time (PoET) Consensus 알고리즘
    - 중앙세서 관리되지 않는 asset ownership... 디지털 레코드
    - 동의 알고리즘이나 스마트 컨트랙트 실행과 같은 분산 원장 문제에 집중
하이퍼레저 이로하 (Hyperledger Iroha)
    - 모바일 어플리케이션 개발에 초점을 둔 분산 원장 개발 프로젝트
    - Byzantine Falut Tolerant 컨센서스 알고리git 즘
하이퍼레저 인디 (Hyperledger Indy)
    - 인증에 특화된 프로젝트
    - 블록체인에 기반한 독립적인 디지털 아이텐티티 레코드 생성
하이퍼레저 버로우 (Hyperledger Burrow)
    - Ethereum Virtual Machine (EVM) 에 기반한 스마트 컨트랙트 인터프리터가 빌트인된 블록체인 클라이언트를 제공
하이퍼레저 베수 (Hyperledger Besu)
    - 엔터프라이즈급 이더리움 코드베이스트 
하이퍼레저 그리드 (Hyperledger Grid)
    - 유통과정 추적이나 선하증권 거래 인증과 같은 공급망 사업 문제를 해결하는 데 중점


### 하이퍼레저 툴 (Hyperledger Tool)
하이퍼레저 캘리퍼 (Hyperledger Caliper)
    - 사전 정의 된 사용 사례 세트를 사용하여 특정 블록 체인 구현의 성능을 측정 할 수 있음
하이퍼레저 첼로 (Hyperledger Cello)
    - as-a-service 디플로이 모델이 가능하게 해줌
    - 블록체인 네트워크 생성, 관리, 삭제 소요되는 노력 최소화
하이퍼레저 익스플로러 (Hyperledger Explorer)
    - 원장에 담긴 정보를 쉽고 빠르게 조회하도록 하는 툴
하이퍼레저 캑터스 (Hyperledger Cactus)
    - 사용자가 다른 블록 체인을 안전하게 통합 할 수 있도록 설계된 블록 체인 통합 도구
하이퍼레저 아발론 (Hyperledger Avalon)
    - 메인 체인에서 블록 컴퓨팅 처리를 전용 컴퓨팅 리소스로 안전하게 이동시키는 것을 목표로 함
하이퍼레저 퀼트 (Hyperledger Quilt)
    - ILP 라는 결재 프로토콜로 원장 시스템간 interoperate를 가능하게 해줌
    - 분산 원장과 일반 원장간의 값 전송이 가능하게 해줌
하이퍼레저 우르사 (Hyperledger URSA)
    - 모듈식의 유연한 공유 암호화 라이브러리
하이퍼레저 에리즈 (Hyperledger Aries)
    - 블록 체인 기반의 P2P 상호 작용을위한 인프라
하이퍼레저 트랜잭트 (Hyperledger Transact)
    - 분산 원장 구현과 별 개인 스마트 계약을 실행하기위한 표준 인터페이스를 제공하여 분산 원장 소프트웨어를 작성하는 개발 노력을 줄이는 것을 목표로 함
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



Single Validating Peers
Multiple Validating Peers
Multichain

