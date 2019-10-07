---
layout: post
title: "BAM: Bottleneck Attention Module 논문 리뷰"
description: 
headline: 
modified: 2019-01-26
category: 논문 리뷰
tags: [DNN, 논문 리뷰, 성능 향상, BAM]
imagefeature: cover3.jpg
mathjax: 
chart: 
share: true
comments: true
---

Deep neural networks의 성능 향상을 도와주는 [BAM : Bottleneck Attention Module](https://arxiv.org/pdf/1807.06514.pdf)을 리뷰를 해보겠다. 

[모두의 연구소 슬로우페이퍼 시즌2](https://event-us.kr/modu/event/4665)에서 논문을 같이 읽고 질문을 나누는 스터디를 진행하는데 앞으로도 여기서 읽은 논문 리뷰를 올릴 생각이다. [한국어 리뷰](https://blog.lunit.io/2018/08/30/bam-and-cbam-self-attention-modules-for-cnn/)와 [논문](https://arxiv.org/pdf/1807.06514.pdf) 그리고 [Github](https://github.com/Jongchan/attention-module)을 참고하여 읽어보자.

![]({{ site.url }}/images/bam8.JPG)  
`ResNet`, `WideResNet`, `PreResNet`, `MobileNet` 등에서 테스트를 통해서 성능향상을 확인했다.


## Introduction, Related Work 간단한 요약

BAM(Bottleneck Attention Module)은 DNN의 성능을 향상해준다. 

**We explicitly investigate the use of attention as a way to improve network’s representational power in an extremely efficient way.**  
네트워크 성능을 효율적으로 향상하는 방법을 조사한다.

**Our main contribution is three-fold.**  
우리의 목표는 3가지다.  
1. 우리는 단순하고 효과적인 모듈인 `BAM`을 제안한다. `CNN`과 쉽게 통합할 수 있다.
2. 광범위한 연구를 통해 `BAM`의 디자인을 검증한다.
3. 여러 `벤치마크` (`CIFAR-100`, `ImageNet-1K`, `VOC 2007` 및 `MS COCO`)에서 다양한 기준 아키텍처를 사용하여 `BAM`의 효율성을 검증합니다.

**We find an efficient location to put our module**  
우리는 모듈을 배치할 수 있는 제일 좋은 위치를 찾았다. 위치는 아래 `Figure. 1`에서 보자.

### Figure 1
![]({{ site.url }}/images/bam9.JPG)  
BAM integrated with a general CNN architecture

기존에 `CNN`과 다른 점은 `BAM 블록`이 있어서 이를 통해서 `DNN`의 성능을 높여준다.

**BAM integrated with a general CNN architecture** 그림과 같이 `BAM`은 네트워크의 모든 병목 지점에 배치된다. 흥미롭게도, 우리는 인간의 지각 과정과 유사한 계층적 주의를 구축하는 여러 BAM을 관찰할 수 있다.

1. `BAM`은 초기 단계에서 배경 텍스처 기능과 같은 저수준 기능을 제거한다. 그러니까 `Hierarchical attention maps` 첫 번째 그림처럼 고양이의 주변 배경들이 제거되고 고양이 모습만 남게 되는 거를 볼 수 있다.
2. 그런 다음 `BAM`은 점차 높은 수준의 정확한 대상에 집중한다. `Intermediate feature maps`부분에 `Stage 3` 그림을 보면 빨간색 초록색 등등 다양한 색을 보이며 `Stage 2`보다 높은 수준의 의미를 이해했다고 볼 수 있다.
3. 점점 더 많은 시각화 및 분석이 포함됩니다. 마지막 그림을 보면 높낮이 등이 포함된 것으로 보이는 더 자세한 내용을 이해했다고 볼 수 있다.

+ `Hierarchical attention maps`이 점점 흐려지는 이유는 학습하면서 점점 pixel이 뭉개지는 것과 범용적으로 쓰기 위해서 일 것이라고 생각한다. 하나의 그림을 그대로 학습하는 것이 아니라 해당하는 그림의 패턴을 찾아서 여러 고양이을 찾기 위해서 일 것이다. 그러므로 점점 패턴으로 `Hierarchical attention maps`이 점점 흐려진다고 생각할 수 있다. 

## 3 Bottleneck Attention Module

### Show, Attend and Tell
![]({{ site.url }}/images/bam3.JPG)  
이미지 출처 : http://kelvinxu.github.io/projects/capgen.html

이 논문에서 `Attention` 즉, 더 집중해야 할 요소에 집중을 하는 모습을 보여준다. 이를 이해하기 쉽게 [Show, Attend and Tell](http://kelvinxu.github.io/projects/capgen.html)를 본다면 각각에 중요한 요소들을 찾는 것을 볼 수 있다.

### 수식

![]({{ site.url }}/images/bam4.JPG)  
`M(F)`를 찾는 수식

`M(F)`는 두 방향으로 연산하는데 결과적으로 [sigmoid function](https://en.wikipedia.org/wiki/Sigmoid_function)을 적용해서 0~1 사이의 값을 가진다.

![]({{ site.url }}/images/bam2.JPG)  
`F'`을 찾는 수식

`F'`은 0~1 사이의 값을 가지는 `M(F)`와 `F`가 ⊗ 연산하고 이전 값과 합친다. 쉽게 생각하면 `M(F)`에서 중요한 부분들을 찾아서 가중치를 높여서 더한다고 생각하면 된다. 


![]({{ site.url }}/images/bam5.JPG)  
Mc(F)를 찾는 수식
 
`channel vector` `Fc`로부터의 채널들에 걸친 중요도를 평가하기 위해, 우리는 하나의 `hidden layer`를 갖는 `MLP(multi-layer perceptron)`를 사용한다.

`MLP` 후에 우리는 `BN(batch normalization)` `layer`를 추가하여 스케일을 조정한다. 

즉, 위 수식의 과정을 정리하면 여러 채널이 있는데 그 채널 중 중요한 채널을 높여서 강조해준다. 이해가 안 된다면 [Show, Attend and Tell](http://kelvinxu.github.io/projects/capgen.html)를 다시 보자.

### Figure 2
![]({{ site.url }}/images/bam6.JPG)

효율적이지만 강력한 모듈을 설계하기 위해, 우리는 branches를 두 개의 나눠서 계산한다. `Mc(F)`(Channel attention)와 `Ms(F)`(Spatial attention)를 먼저 계산하고 결과 값을 더하고 `sigmoid function`을 적용해 `M(F)`(BAM attention)을 만든다. 그 후는 위에서 설명한 `F'`을 찾는 수식에서 설명한 행위를 실행한다.

![]({{ site.url }}/images/bam2.JPG)  
`F'`을 찾는 수식

`Figure 2`는 위 수식을 그림으로 자세히 설명한 것이다.

`Ms(F)`(Spatial attention)는 의미를 유지하기 위해 `1 X H X W`로 만든다. 마지막에 `1 X 1 CONV`로 `Rc` 부분을 1로 바꾼 것을 제외하면 기본적인 `CNN`과 비슷한 연산을 한다.

![]({{ site.url }}/images/bam7.JPG)  
사진 출처 : https://alexisbcook.github.io/2017/global-average-pooling-layers-for-object-localization/

`Mc(F)`(Channel attention)는 [Global avg pool](https://alexisbcook.github.io/2017/global-average-pooling-layers-for-object-localization/)을 통해서 `H X W`를 `1 X 1`로 바꾼다.

### branches를 두 개로 나눈 이유

예를 들어 `1000 X 1000 X 1000`의 network를 연산한다면 엄청난 연산과 [overfitting](https://en.wikipedia.org/wiki/Overfitting)이 발생할 수 있다. 하지만 만약에 2개로 나누면 `1 X 1000 X 1000`과 `1000 X 1 X 1`를 더하면 되는 것으로 훨씬 간단하게 연산을 수행할 수 있다.

### 궁금한 점

`Sigmoid`는 항상 0~1 값으로 즉, `F\'= F+F⊗M(F)`에서는 값이 -가 되지 않는다. [Tanh](https://en.wikipedia.org/wiki/Hyperbolic_function)를 한다면 -가 될 수도 있는데 말이다. `M(F)`에서 `Sigmoid`를 사용하기에 항상 +가 돼서 값이 계속 올라가는 것만 가능한데 왜 그렇게 하는지 모르겠다. 그리고 다른 논문들도 `Sigmoid`를 많이 사용하는데 이유가 있는 것인지, `Sigmoid`가 편해서 인지 모르겠다.

## 4 Experiments

![]({{ site.url }}/images/bam10.JPG)  
4.1 Ablation studies on CIFAR-100

![]({{ site.url }}/images/bam11.JPG)  
4.1 Ablation studies on CIFAR-100

![]({{ site.url }}/images/bam8.JPG)  
4.1 Ablation studies on CIFAR-100

![]({{ site.url }}/images/bam12.JPG)  
4.3 Classification Results on ImageNet-1K

![]({{ site.url }}/images/bam13.JPG)  
4.6 VOC 2007 Object Detection


`BAM` 적용으로 각종 실험에서 1% 정도 수준의 성능 향상이 있는 것을 확인할 수 있다.

## Conclusion

`BAM` 적용을 적용하면 여러 `vision` 작업에서 성능향상이 가능할 것으로 보인다. 그리고 **궁금한 점**에서 이야기한 `Tanh`를 적용해보는 테스트해 볼 예정이다. 만약에 성능향상이 더 된다면 새로운 논문을 쓸 수 있지 않을까?

첫 번째 논문 리뷰로 부족한 점이 많을 거 같다.