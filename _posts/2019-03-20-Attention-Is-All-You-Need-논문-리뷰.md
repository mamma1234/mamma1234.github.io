---
layout: post
title: "Attention Is All You Need 논문 리뷰"
description: 
headline: 
modified: 2019-03-20
category: 논문 리뷰
imagefeature: cover3.jpg
tags: [논문 리뷰, attention, neural machine translation]
mathjax: 
chart: 
share: true
comments: true
---

RNN이나 CNN이 아닌 새로운 구조를 개척한 [Attention Is All You Need](https://arxiv.org/pdf/1706.03762.pdf)을 리뷰를 해보겠다. 

![]({{ site.url }}/images/Attention_Is_All_You_Need1.JPG)  
특이한 구조를 가지고 있다.

[한국어 리뷰1](https://dalpo0814.tistory.com/49), [한국어 리뷰2](https://pozalabs.github.io/transformer/), [논문](https://arxiv.org/pdf/1706.03762.pdf)을 참고하자.

## ABSTRACT

`sequence transduction models`는 `encoder and a decode`를 포함하는 복잡한 `recurrent or convolutional neural networks`에 기초한다. 가장 성능이 좋은 모델은 `attention mechanism`을 통해 `encoder and decode`를 연결한다. 우리는 `recurrence and convolutions neural networks`를 제거하고 오로지 `attention mechanisms`에만 기초한 새롭고 간단한 `network` 구조를 제안한다. 

`machine translation` 작업에 대한 실험 결과를 보면 이 모델은 병렬 처리가 가능하고 학습 시간이 훨씬 덜 소요되는 동시에 품질이 우수한 것을 확인했다. 그리고 2014년 `WMT Englishto-German` 번역 대회에서 `28.4 BLEU`를 달성하면서 기존 최고 모델보다 `2BLEU` 이상 향상하며 `state-of-the-art`를 달성했다.

우리는 `Transformer`가 크고 제한된 훈련 자료로 영어 문법 해석에 성공적으로 적용됨으로써 다른 `tasks`에서도 잘 일반화됨을 보여준다.

## Introduction

`RNN`, `LSTM`, `GRU`는 언어 모델링 및 기계 번역과 같은 시퀀스 모델링 문제에서 확고히 자리를 잡았다. 하지만 `Recurrent` 모델은 필연적으로 이전 결과를 입력으로 받는 순차적 특성 때문에 병렬처리를 배제한다. 최근의 연구는 `factorization tricks`과 `conditional computation`을 통해 연산 효율의 대폭적인 향상을 달성했다. 하지만 아직까지 순차적 계산의 근본적인 제약은 여전히 남아있다.

아직까지도 (이 논문은 2017년에 작성되었다) 대부분은 `attention mechanisms`도 `recurrent network`와 함께 사용된다.

우리는 `Recurrent` 모델의 제약 사항들을 피하고 입력과 출력 사이에 전역 의존성을 이끌어내기 위해 `Transformer`을 제안한다. (`Transformer`은 병렬화가 가능하고 높은 성능을 자랑한다)

## Model Architecture

![]({{ site.url }}/images/Attention_Is_All_You_Need1.JPG)  
`Attention`만으로 `encoder-decoder` 구조를 가진 모델

### Encoder
- `Encoder`는 `N = 6`개의 동일한 층으로 구성되어 있다. 처음 `input`이 첫 번째 층에 들어가고 그 다음 층은 이전 층의 결과값이 들어가는 식이다.
- 각 층에는 2개의 `sub-layers`가 있다. 첫 번째는 `multi-head self-attention`이고 두 번째는 단순하게 완전 연결된 `feed-forward`이다. 
- 우리는 2개의 `sub-layers` 주의에 `residual connection`을 채택하고 있다. 그리고 `layer normalization`를 진행한다. 
- 각 `sub-layers`의 출력은 `LayerNorm(x + Sublayer(x))`이다. 이러한 `residual connections`을 용이하게 하기 위해 모델의 모든 레이어는 `512 차원`으로 임베딩한다.

### Decoder
- `Decoder`도 `Encoder`와 같이 `N = 6`개의 동일한 층으로 구성되어 있다. 이외에도 `residual connection`을 수행한 후 `layer normalization`을 진행하는 것도 동일하다.
- `Decoder`는 각 층에는 2개의 `sub-layers` 이외에도 `Encoder` 스택의 출력을 통해 `multi-head self-attention`을 수행하는 3번째 `sub-layers`를 삽입한다.
- 또 다른 점은 `Decoder`는 순차적으로 결과를 만들어야 한다. `masking`을 통해 `position i`보다 작은. 즉, 미리 알고 있는 `output`들에만 의존한다.

![]({{ site.url }}/images/Attention_Is_All_You_Need.gif)  
그림을 통해서 해당 모델이 어떤 식으로 동작하는지 살펴보자.

## Attention
[이전 논문 리뷰](https://newhiwoong.github.io/%EB%85%BC%EB%AC%B8%20%EB%A6%AC%EB%B7%B0/NEURAL-MACHINE-TRANSLATION-BY-JOINTLY-LEARNING-TO-ALIGN-AND-TRANSLATE-%EB%85%BC%EB%AC%B8-%EB%A6%AC%EB%B7%B0)에서 `Attention`에 대한 개념을 다뤘으니 참고하길 바란다. 여기서 나올 `query, keys, values`는 각각 `previous layer의 hidden state`, 이 값들을 통해 `Attention`을 계산한다.

### Scaled Dot-Product Attention

![]({{ site.url }}/images/Attention_Is_All_You_Need2.JPG)  

우리의 특별한 `attention`을 `"Scaled Dot-Product Attention"`이라고 부른다. 

![]({{ site.url }}/images/Attention_Is_All_You_Need4.JPG)  
식은 다음과 같다.

입력은 `dk` 차원의 `query`와 `key` 그리고 `dv` 차원의 `value`들로 있다. 이하 `Q, K, V`로 부른다. 먼저 `Q`와 `K`를 `dot products`하고 `√dk`로 나눈다. 그 후 `softmax` 함수를 적용해서 `value`에 대한 `weights`를 얻어낸다. 즉 `Q, K`에 맞게 `V`에 `attention`을 주는 방식으로 이해했다.

`dot products`값이 모두 너무 크다면 `softmax`의 기울기가 작아지기 때문에 `1 / √dk `로 `dot products`한 값을 `scale`한다.

```
여기서 Q, K, V란?
“encoder-decoder attention”의 경우, 
Q : 디코더의 이전 레이어 hidden state 
K : 인코더의 output state 
V : 인코더의 output state 

“self-attention”의 경우, 
Q=K=V : 인코더의 output state

출처: https://dalpo0814.tistory.com/49 [deeep]
```

### Multi-Head Attention

![]({{ site.url }}/images/Attention_Is_All_You_Need3.JPG)  

`dmodel-dimensional`의 `keys, values, queries`로 단일 `attention function`를 수행하는 것 보다, `dk, dk, dv` 차원에 대해 학습된 `keys, values, queries Linear`를 `h번` 계산하는 것이 더 좋다고 한다. 이유는 각 벡터들의 크기들을 줄이고 병렬처리가 가능하기에 더 낫다.

![]({{ site.url }}/images/Attention_Is_All_You_Need5.JPG)  
각각의 `head` 즉 `keys, values, queries`을 `h개`로 나눈 값들의 `attention`을 구하고 `Concat`한다. 

### Position-wise Feed-Forward Networks

`attention sub-layers` 외에도, `encoder`와 `decoder`의 각 `layer`는 `fully connected feed-forward network`를 포함하고 있으며, 이것은 `ReLU`를 활성함수로 사용하는 두번의 `linear transformations`으로 구성된다.

![]({{ site.url }}/images/Attention_Is_All_You_Need6.JPG)  

### Positional Encoding

우리 모델은 `rnn`이나 `cnn`이 아니기에 순서에 따라, 시퀀스의 위치에 관한 정보를 주입해야한다. 이를 위해 인코더 및 디코더 스택 하단에 `positional encodings`을 추가한다. `positional encodings`은 `dmodel(embedding)`과 동일한 차원을 갖어 이를 더하는 작업을 할 수 있다.

![]({{ site.url }}/images/Attention_Is_All_You_Need7.JPG)  
위 식을 이용해서 `Positional Encoding`을 하고 위치 관련된 정보를 주입할 수 있다.

## Why Self-Attention
1. 레이어당 계산양이 줄어든다. (n이 d보다 훨씬 작으니까)
2. 병렬처리가 가능한 계산이 늘어난다.
3. 장거리 학습의 가능 여부이다. `Attention`을 통해 모든 부분을 확인하니 `rnn`에 보다 훨씬 먼 거리에 있는 시퀀스를 잘 학습할 수 있다.

![]({{ site.url }}/images/Attention_Is_All_You_Need8.JPG)  
다른 기법들과 `Self-Attention`을 비교한 표

또한 `restricted`을 이용하여 시퀀스 길이 `n`이 클때 `r`크기의 주변만 고려하는 것으로 제안할 수 있다. [관련 논문](https://arxiv.org/pdf/1508.04025.pdf)

다른 이점으로는, self-attention은 문장의 통사적, 의미적 구조를 해석 가능한 모델을 만들 수 있다.

![]({{ site.url }}/images/Attention_Is_All_You_Need9.JPG)  
예를 들어 여기서 `its`가 지칭하는 부분들이 얼마나 유사한지를 시각화하여 문장 내에서의 관계를 해석할 수 있다.

## Training

`WMT 2014 English-German dataset`을 사용했다. `NVIDIA P100 GPUs` 8대로 기본 모델은 12시간 동안을 `big` 모델은 3.5일을 학습시켰다.

![]({{ site.url }}/images/Attention_Is_All_You_Need10.JPG)  
성능에 비해 빠른 속도로 우수한 `BLEU scores`를 획득했다. 그리고 `EN-DE`에서는 당시 `state-of-the-art`를 달성했다. 
