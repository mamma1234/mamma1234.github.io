---
layout: post
title: "Kubernetes"
description: 
headline: 
modified: 2020-03-13
category: webdevelopment
imagefeature: cover3.jpg
tags: [Kubernetes 쿠버네티스]
mathjax: 
chart: 
share: true
comments: true
featured: false
disqus:
---
# Kubernetes
분산 시스템에서 컨테이너를 운용하기 위한 노하우로 가득 채워진 세련된 오픈소스 소프트웨어

쿠버네티스는 컨테이너화된 워크로드와 서비스를 관리하기 위한 이식성이 있고, 확장가능한 오픈소스 플랫폼이다. 쿠버네티스는 선언적 구성과 자동화를 모두 용이하게 해준다. 쿠버네티스는 크고, 빠르게 성장하는 생태계를 가지고 있다. 쿠버네티스 서비스, 기술 지원 및 도구는 어디서나 쉽게 이용할 수 있다.

쿠버네티스란 명칭은 키잡이(helmsman)나 파일럿을 뜻하는 그리스어에서 유래했다. 구글이 2014년에 쿠버네티스 프로젝트를 오픈소스화했다. 쿠버네티스는 프로덕션 워크로드를 대규모로 운영하는 15년 이상의 구글 경험과 커뮤니티의 최고의 아이디어와 적용 사례가 결합되어 있다.

- 서비스 디스커버리와 로드 밸런싱
- 스토리지 오케스트레이션 
- 자동화된 롤아웃과 롤백 
- 자동화된 빈 패킹(bin packing)
- 자동화된 복구(self-healing) 
- 시크릿과 구성 관리 


## 쿠버네티스 장점 3가지
1. 컨테이너관리
2. 로드밸런싱
3 .롤링업데이트

## 스케줄링
- 애플리케이션을 적절한 곳에 디플로이하는 장치를 스케줄링(scheduling)

## 오케스트레이션
## 클러스터링
## 서비스 매시
    Service Discovery (서비스 발견)
    Load Balancing (부하 분산)
    Routing Management (경로 관리)
    Traffic Management (트래픽 관리)
    Resilient (운영 탄력성)
    Fault Injection (오류 주입)
    Logging / Monitoring (로깅/모니터링)
    Distributed Tracing (분산 추적)
    Security (보안)
    Authentication, Authorization (인증, 인가)

## 서비스 디스커버리
- 서비스간의 호출은 서비스 디스커버리가 수행
- 고정 IP 주소 : 서비스 고정 IP주소를 결정
- 호스트 파일의 엔트리 : 파일을 사용하여 서버명과 P주소를 매핑
- DNS : 서버를 사용하여 도메인명과 IP 주소를 매핑
- 구성 레지스트리 : 인프라스트럭처와 서비스를 연결하여 일원 관리

### Pod
파드(Pod) 는 쿠버네티스에서 생성하고 관리할 수 있는 배포 가능한 가장 작은 컴퓨팅 단위이다.

파드 (고래 떼(pod of whales)나 콩꼬투리(pea pod)와 마찬가지로)는 하나 이상의 컨테이너의 그룹이다. 이 그룹은 스토리지/네트워크를 공유하고, 해당 컨테이너를 구동하는 방식에 대한 명세를 갖는다. 파드의 콘텐츠는 항상 함께 배치되고, 함께 스케줄되며, 공유 콘텍스트에서 실행된다. 파드는 애플리케이션 별 "논리 호스트"를 모델링한다. 여기에는 상대적으로 밀접하게 결합된 하나 이상의 애플리케이션 컨테이너가 포함된다. 클라우드가 아닌 콘텍스트에서, 동일한 물리 또는 가상 머신에서 실행되는 애플리케이션은 동일한 논리 호스트에서 실행되는 클라우드 애플리케이션과 비슷하다.

애플리케이션 컨테이너와 마찬가지로, 파드에는 파드 시작 중에 실행되는 초기화 컨테이너가 포함될 수 있다. 클러스터가 제공하는 경우, 디버깅을 위해 임시 컨테이너를 삽입할 수도 있다


값	의미	
    - Pending	파드가 쿠버네티스 클러스터에서 승인되었지만, 하나 이상의 컨테이너가 설정되지 않았고 실행할 준비가 되지 않았다. 여기에는 파드가 스케줄되기 이전까지의 시간 뿐만 아니라 네트워크를 통한 컨테이너 이미지 다운로드 시간도 포함된다.
	- Running	파드가 노드에 바인딩되었고, 모든 컨테이너가 생성되었다. 적어도 하나의 컨테이너가 아직 실행 중이거나, 시작 또는 재시작 중에 있다.	Succeeded	파드에 있는 모든 컨테이너들이 성공적으로 종료되었고, 재시작되지 않을 것이다.	
    - Failed	파드에 있는 모든 컨테이너가 종료되었고, 적어도 하나 이상의 컨테이너가 실패로 종료되었다. 즉, 해당 컨테이너는 non-zero 상태로 빠져나왔거나(exited) 시스템에 의해서 종료(terminated)되었다.	
    - Unknown	어떤 이유에 의해서 파드의 상태를 얻을 수 없다. 이 단계는 일반적으로 파드가 실행되어야 하는 노드와의 통신 오류로 인해 발생한다.


#### 컨테이너 상태
- Waiting
만약 컨테이너가 Running 또는 Terminated 상태가 아니면, Waiting 상태이다. Waiting 상태의 컨테이너는 시작을 완료하는 데 필요한 작업(예를 들어, 컨테이너 이미지 레지스트리에서 컨테이너 이미지 가져오거나, 시크릿(Secret) 데이터를 적용하는 작업)을 계속 실행하고 있는 중이다. kubectl 을 사용하여 컨테이너가 Waiting 인 파드를 쿼리하면, 컨테이너가 해당 상태에 있는 이유를 요약하는 Reason 필드도 표시된다.

- Running
Running 상태는 컨테이너가 문제없이 실행되고 있음을 나타낸다. postStart 훅이 구성되어 있었다면, 이미 실행이 완료되었다. kubectl 을 사용하여 컨테이너가 Running 인 파드를 쿼리하면, 컨테이너가 Running 상태에 진입한 시기에 대한 정보도 볼 수 있다.

- Terminated
Terminated 상태의 컨테이너는 실행을 시작한 다음 완료될 때까지 실행되었거나 어떤 이유로 실패했다. kubectl 을 사용하여 컨테이너가 Terminated 인 파드를 쿼리하면, 이유와 종료 코드 그리고 해당 컨테이너의 실행 기간에 대한 시작과 종료 시간이 표시된다.

컨테이너에 구성된 preStop 훅이 있는 경우, 컨테이너가 Terminated 상태에 들어가기 전에 실행된다


##### 컨테이너 프로브(probe)

프로브는 컨테이너에서 kubelet에 의해 주기적으로 수행되는 진단(diagnostic)이다. 

- Success: 컨테이너가 진단을 통과함.
- Failure: 컨테이너가 진단에 실패함.
- Unknown: 진단 자체가 실패하였으므로 아무런 액션도 수행되면 안됨.


## 스테이트풀셋

### 디플로이먼트와 스케일링 보증 


### kubeadm
kubernetes 클러스터를 구축하기 위해 사용하는 툴이다.
kubeadm이란, kubernetes에서 제공하는 기본적인 도구이며, kubernetes 클러스터를 가장 빨리 구축하기 위한 다양한 기능을 제공한다.

#### kubeadm init
- Kubernetes 컨트롤 플레인 노드를 초기화한다.
- 즉, 마스터 노드를 초기화한다.

#### kubeadm join
- Kubernetes 워커 노드를 초기화하고 클러스터에 연결한다.

#### kubeadm upgrade
- Kubernetes 클러스터를 업그레이드 한다.

#### kubeadm config

#### kubeadm token
- 부트 스트랩 토큰을 사용한 인증에 설명된대로 부트 스트랩 토큰은 클러스터에 참여하는 노드와 제어 평면 노드 사이에 양방향 신뢰를 설정하는 데 사용된다.

#### kubeadm reset
- kubeadm init 혹은 kubeadm join의 변경사항을 최대한 복구한다.

#### kubeadm version
- kubeadm 버젼은 보여준다.

#### kubeadm alpha
- 정식으로 배포된 기능은 아니지만 kubernetes측에서 사용자 피드백을 얻기 위해 인증서 갱신, 인증서 만료 확인, 사용자 생성, kubelet 설정 등 다양한 기능을 제공하고 있다.


### kubelet
클러스터의 모든 머신에서 실행되며 Pod 및 컨테이너 시작 등의 작업을 수행하는 구성 요소이다.

### kubectl
클러스터와 통신하는 커맨드라인 인터페이스 유틸이다.
```JavaScript
 각 노드와 상태를 확인할 수 있습니다
    kubectl get no
    NAME       STATUS   ROLES    AGE     VERSION
    master     Ready    master   6m44s   v1.13.3
    worker-1   Ready    <none>   5m20s   v1.13.3
    worker-2   Ready    <none>   5m19s   v1.13.3
```

## 각 노드와 상태를 확인
```JavaScript
 각 노드와 상태를 확인할 수 있습니다
    kubectl get no
    NAME       STATUS   ROLES    AGE     VERSION
    master     Ready    master   6m44s   v1.13.3
    worker-1   Ready    <none>   5m20s   v1.13.3
    worker-2   Ready    <none>   5m19s   v1.13.3
```

## 설치 확인하기
```JavaScript
kubectl get componentstatuses
NAME                 STATUS    MESSAGE              ERROR
scheduler            Healthy   ok                   
controller-manager   Healthy   ok                   
etcd-0               Healthy   {"health": "true"}
```

## Pod 을 배포
```JavaScript
    apiVersion: v1
    kind: Pod
    metadata:
    name: myapp-pod
    labels:
        app: myapp
    spec:
    containers:
    - name: myapp-container
        image: busybox
        command: ['sh', '-c', 'echo Hello Kubernetes! && sleep 3600']

    kubectl apply -f pod-test.yaml
```

## Pod 이 정상적으로 실행 확인
```JavaScript
    kubectl get po
    NAME        READY   STATUS    RESTARTS   AGE
    myapp-pod   1/1     Running   0          6s
```

## 로그 확인
```JavaScript
    kubectl logs myapp-pod
    Hello Kubernetes!
```

## 로그 확인
```JavaScript
    kubectl describe pod nginx-test
    kubectl logs nginx-test
    kubectl get pods --all-namespaces
    kubectl get events
```


## Kubernetes 종료
- 쿠버네티스 클러스터를 삭제하는 방법입니다
```JavaScript
Master에서 :
$ kubectl drain {노드이름} --delete-local-data --force --ignore-daemonsets
$ kubectl delete node {노드이름}

$ kubeadm reset

Node에서 :
$ kubeadm reset
```


노드	| 프로토콜	| 방향	| 포트 범위	| 목적	| 누가 사용?
Master	| TCP	| Inbound	| 6443	| Kubernetes API server	| All
Master	| TCP	| Inbound	| 2379-2380	| etcd server client API	| kube-apiserver, etcd
Master	| TCP	| Inbound	| 10250	| Kubelet API	| Self, Control plane
Master	| TCP	| Inbound	| 10251	| kube-scheduler	| Self
Master	| TCP	| Inbound	| 10252	| kube-controller-manager	| Self
Worker	| TCP	| Inbound	| 10250	| Kubelet API	| Self, Control plane
Worker	| TCP	| Inbound	| 30000-32767 | NodePort Services	| All