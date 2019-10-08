---
layout: post
title: "Language Models are Unsupervised Multitask Learners, GPT-2 논문 리뷰"
description: 
headline: 
modified: 2019-04-29
category: 논문 리뷰
imagefeature: cover3.jpg
tags: [논문 리뷰, NLP, Language model]
mathjax: 
chart: 
share: true
comments: true
---

엄청난 퀄리티로 텍스트를 재생산하는 OpenAI에서 공개한 [Language Models are Unsupervised Multitask Learners](https://d4mucfpksywv.cloudfront.net/better-language-models/language_models_are_unsupervised_multitask_learners.pdf)을 리뷰를 해보겠다. 

![]({{ site.url }}/images/GPT-2.JPG)  
정말로 이정도 퀄리티의 문장을 만들 수 있을지 궁금하다. 동시에 한글로 구현할 수 있으면 좋겠다는 생각이 들었다.

[한국어 리뷰1](https://ai-information.blogspot.com/2019/02/language-models-are-unsupervised_21.html), [논문](https://d4mucfpksywv.cloudfront.net/better-language-models/language_models_are_unsupervised_multitask_learners.pdf)을 참고하자.

## ABSTRACT

여러 NLP task는 supervised learning 으로 특정 task에 맞는 datasets을 가지고 접근했다. 우리는 WebText라고 불리는 수백만 웹 페이지의 데이터로 explicit supervision 없이 language models을 학습한다. language model은 zero-shot task가 필수적이며, 이를 늘리면 log-linear 방식으로 성능이 향상된다. 우리의 모델 GPT-2는 1.5B parameter를 가진 Transformer이며, language modeling datasets 8개중 7개를 zero-shot setting으로 state of the art을 달성했다.

## Introduction

- 일반적인 ML은 데이터의 영향을 많이 받고 레이블링이 필요함. 거기다 레이블도 데이터의 균형이 필요. 우린 레이블링 없이 모든 작업을 잘하는 애를 만들고 싶음.
- 다양한 작업에서 기존의 훈련 데이터를 모방하는 방법의 문제를 발견했다.
- Multitask learning이 일반화를 잘하는데 유망한 프레임워크이다. NLP에서는 아직 초기 단계다. 대신 많은 효과적인 훈련 쌍을 필요하다.
- 이전에는 테스크 마다 다른 방식이 필요했는데, 최근에는 self-attention이면 충분하다.
- 상식 추리, 감성 분석은 no supervised로도 꽤 괜찮은 성능을 보인다.
- zero-shot setting으로 광범위한 작업을 수행하는 언어 모델의 능력을 강조하고 잠재력을 보여준다.

## Approach

- 우리의 접근 방식은 LM이다. LM은 비지도 분포 추정으로 어떤 테스트 세트에서도 적용이 가능하다.
- 이런 방식은 tractable sampling이 가능하고 Transformer 같은 self-attention으로 표현성이 높아짐.
- 단일 과제 수행법을 배우는 것은 조건부 분포를 추정하는 것으로 확률론적 프레임워크로 표현 가능. 
- 일반 시스템은 동일한 입력에 대해서도 여러 가지 다양한 작업을 할 수 있어야됨. 그러니까 수행할 작업에 대해서도 조건을 달아야 한다. p(output, task)를 모델로 삼아야 한다. (결과 뿐만 아니라 task도)
- McCann에서 단일 모델 MAQN을 훈련해서 다양한 형식의 예에서 많은 작업을 유추하고 수행할 수 있는 것을 보여줌.
- 우리는 LM이 parameter나 아키텍처 수정 없이 zero-shot setting으로 높은 성능을 보이며, LM의 능력을 강조함으로써 가능성을 보여준다.

### Training Dataset

- 데이터 셋은 매우 중요. garbage in, garbage out 이니까. 
- 기존 데이터들에 문제가 있어서 직접 크롤러를 제작함. (말이 안 되거나 중복 등)
- Reddit에서 3 karma 이상을 받은 데이터들만 크롤링함.
- 결과적으로 45 million개의 links 중 아래와 같은 것들을 추출
- 2017년 12월 전에 post만 가지고 Dragnet과 텍스트만 페어로 크롤링, 
- 위키피티아와 중복 되는 부분을 삭제하고 총 40GB text, 총 8 million개의 문서 생성

### Input Representation

- Byte Pair Encoding (BPE) 는 character, word level의 중간 지점 
- 다중 기호 토큰을 추가하기 전에 13만 개 이상의 기본 어휘를 얻게 된다.
- 32,000에서 64,000개의 토큰 단어들과 비교했을 때 엄청나게 크다.
- 대조적으로, BPE의 바이트 레벨 버전은 256 크기의 기본 어휘만 요구한다.
- dog. dog! dog? 같은 많은 변형에서 발생하기 때문에 개와 같은 일반적인 단어들의 많은 버전을 포함하는 것을 관찰했다. 
- 여러 개의 단어 토큰에 단어 조각만 최소화하는 동시에 압축 효율을 크게 향상시키는 공간에 대한 예외를 추가한다.
- BPE 알고리즘의 기본 원리는 가장 많이 등장한 문자열에 대하여 병합 하는 작업을 반복하는데, 원하는 단어 집합의 크기. 즉, 단어의 갯수가 될 때까지 이 작업을 반복한다.
- 워드 레벨 LM의 경험적 편익과 바이트 레벨 접근법의 일반성을 결합할 수 있다.
- 우리의 접근방식은 어떤 유니코드 문자열에도 확률을 할당할 수 있기에  pre-processing, tokenization, vocab size 관계 없이 모든 데이터셋에서 우리의 LM을 평가할 수 있게 해준다.

### Model

- normalization 레이어를 각 하위 블록의 입력으로 이동
- 마지막 셀프 어텐션 모델 이후의 normalization 레이어 추가
- 모델 깊이가 있는  residual layers 축적을 설명하는 수정된 초기화가 사용된다. 초기화 시 1/√N의 비율로 조정, N은 residual layers 수 (스케일링 느낌)
- context size를 512 -> 1024 tokens으로 512 더 큰 batchsize 사용.
- 다른 시나리오에 맞추기 위해 다른 매개 변수가있는 4 개의 모델을 학습.

## Experiments

- 4개로 실험하고 아래에 표가 있음.
- 가장 작은애의 크기가 GPT, 2번째 작은애의 크기가 가장 큰 BERT, 가장 큰 모델이 15억 파라미터.

### Language Modeling

- 8개 중에 7개의 LM dataset에서 zero-show으로 SOTA 만듬.
- 소규모 데이터 셋에서 큰 개선이 모임.
- 하지만 우리의 모델은 여전히 10억 단어 벤치마크에 대한 이전 작업보다 훨씬 더 나쁘다. 이는 가장 큰 데이터셋과 가장 파괴적인 전처리(pre-processing)가 결합된 결과일 가능성이 높다. 1BW의 문장 수준 셔플링은 모든 장거리 구조를 제거한다. 

### 이 외의 다른 테스트들

- 다음 문장이 명사, 동사, 전치사 인지 잘 평가하는가
- 50개 토큰의 컨텍스트를 필요로 하는 문장의 마지막 단어 예측
- 문맥화 해서 모호성 낮추기
- CoQA로 QA 테스트 제로샷으로 베이스라인 시스템 4개 중 3개보다 성능이 높음. 인간의 가까운 bert보다는 낮음.
- CNN과 Daily Mail dataset에서 요약 능력 테스트 100개의 토큰을 생성 처음 3개의 문장을 요약으로 사용, 베이스 라인 보다 살짝 좋은 정도 
- 10MB으로 영어 - 프랑스어를 11.5BLEU 달성
- QA에서 질문의 4.1%를 정확하게 답한다. 그리고 GPT-2는 가장 자신 있는 1%의 질문에서 63.1%의 정확도를 갖는다. 

## Generalization vs Memorization
- 현재 데이터에는 문제가 있음. 데이터 중첩 문제가 있으면 test와 train에 같은 데이터가 있으면 과평가가 가능.
- WebText가 워낙 크다 보니까. 테스트를 하는 여러 테스크에 있는 것들이 이미 중복이 됐을 가능성이 있음.
- Bloon filter와 8-gram을 사용해서 겹치는 데이터를 확인. 
- overlap, similar text 가 학습에 끼치는 영향을 알아내는 것은 중요.
- 결과적으로 중복 그러니 중첩이 된 것들이 있음
- 매우 유사한 텍스트가 성능에 미치는 영향을 이해하고 수량화하는 것은 중요한 연구 질문이다. 
- 현재로서는 n-gram 중첩 기반 중복 제거를 중요한 검증 단계와 새 NLP 데이터 세트의 교육 및 테스트 분할 생성 시 무결성 점검으로 사용할 것을 권장한다.
- 모델 크기의 함수로 WebText에서 훈련된 LM의 성능을 그래프로 보면, train과 test 모두 perplexity가 떨어진다. 즉 GPT-2조차 아직 underfitting이 됨을 알 수가 있다.

## Discussion

- 우리의 결과는 unsupervised task learning이 탐구해야 할 추가적인 유망한 연구 영역임을 시사한다.
- gpt-2의 결과를 통해서 NLP 분야에서 supervised adaption에서 수정 없이 pre-training로 할 수 있다는 가능성을 보여줌.
- Supervision 없이 task를 배우는 pre-training 기술도 가능성 있다.
- 그러나, 요약과 같은 다른 과제에 대해서는, 여전히 초보적인 수준에 불과하다. 
- 연구 결과로서 시사하는 바는 있지만, 실용적 적용 측면에서 GPT-2의 제로샷 성능은 아직 사용한 수준은 아니다.
- GPT-2의 성능이 여전히 무작위적인 것과 다를 바 없는 다른 말로 성능이 매우 낮은 많은 실질적인 과제들이 있다.
- 우리는 많은 일반적인 NLP 작업에서 WebText LM의 제로샷 성능을 연구해 왔지만, 평가될 수 있는 많은 추가적인 과제가 있다. 
- 제로샷 성능은 많은 과제에서 GPT-2의 잠재적 성능의 기준을 설정하지만, finetuning의 최대 한계가 어디에 있는지 명확하지 않다. 
- GPT-2의 추가 훈련 데이터와 용량이 BERT(Devlin et al., 2018)에서 입증된 단방향 표현의 비효율성을 극복하기에 충분한지 불분명하기 때문에 decaNLP, GLUE 등의 벤치마크에 대한 정밀 조율을 조사할 계획이다.

## Conclusion

많은 연구들은 지도 또는 비지도 선행 트레이닝 방법의 재현에 대한 학습, 이해, 비판적 평가에 기여해온 것이 사실이다. 우리의 연구 결과는 비지도 작업 학습이 연구로서 탐구해볼 유망한 영역임을 말해주고 있다.

대형 언어 모델이 충분히 크고 다양한 데이터셋에서 훈련될 때, 도메인 및 데이터셋에서 잘 수행될 수 있다.

GPT-2 테스트된 언어 모델링 데이터 세트 8개 중 7개에서 예술 성능을 제로샷으로 만들었다. 

모델이 제로샷 설정에서 수행할 수 있는 작업의 다양성은 충분히 다양한 텍스트 코퍼스의 가능성을 극대화하기 위해 훈련된 고용량 모델이 명시적인 감독 없이 놀라운 양의 작업을 수행하는 방법을 배우기 시작함을 시사한다.

우리는 여러 기본적인 NLP 작업에서 WebText 언어모델의 제로샷 수행을 연구했지만, 아직 평가해야만 하는 여러 부가적 작업이 남아있다.

