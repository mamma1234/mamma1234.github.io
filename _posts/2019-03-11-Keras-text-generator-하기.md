---
layout: post
title: "Keras text generator 하기"
description: 
headline: 
modified: 2019-03-11
category: Keras
tags: [Keras, LSTM, Generator, NLP]
imagefeature: 
mathjax: 
chart: 
share: true
comments: true
---

Keras로 간단한 [text generator](https://github.com/newhiwoong/Keras-Applications/blob/master/12_Generation_text_with_lstm.ipynb)을 구현해보겠다. 이 예제는 [Keras examples code](https://github.com/keras-team/keras/blob/master/examples/lstm_text_generation.py)로 작성되었다. 그리고 post내용은 [케라스 창시자에게 배우는 딥러닝](https://github.com/rickiepark/deep-learning-with-python-notebooks)의 내용이다.

# 이론 

---

## 시퀀스 데이터를 어떻게 생성할까?

딥러닝에서 시퀀스 데이터를 생성하는 일반적인 방법은 이전 토큰을 입력으로 사용하여 `시퀀스`의 다음 1개 또는 몇 개의 토큰을 예측하는 것이다. 예를 들어 `the cat is on ma`란 입력이 주어지면 다음 글자인 타깃 `t`를 예측하도록 `네트워크`를 훈련한다. 텍스트 데이터를 다룰 때 토큰은 보통 단어 또는 글자이다. 이전 토큰들을 줬을 때 다음 토큰의 `확률을 모델링`할 수 있는 `네트워크`를 `언어 모델`이라고 부른다. `언어 모델`은 언어의 통계적 구조인 `잠재 공간`을 탐색한다.

초기 텍스트 문자열을 주입하고(`conditioning data`) 새로운 글자나 단어를 생성한다. 생성된 출력은 다시 입력 데이터로 추가된다. 이 과정을 여러 번 반복한다. 이런 반복을 통해 모델이 훈련의 비슷한 `시퀀스`를 만든다. 텍스트 말뭉치(`corpus`)에서 `N`개의 글자로 이루어진 문자열을 추출하여 주입하고 `N + 1`번째 글자를 예측하도록 훈련한다. 모델의 출력은 출력 가능한 모든 글자에 해당하는 `소프트맥스` 값이다. 즉 다음 글자의 확률 분포이다. 이 `LSTM`을 글자 수준의 신경망 언어 모델(`character-level neural language model`)이라고 부른다.

## 샘플링 전략의 중요성

텍스트를 생성할 때 다음 글자를 선택하는 방법은 매우 중요하다. 가장 높은 확률을 가진 글자를 선택하는 탐욕적 샘플링(`greedy sampling`)과 다음 글자의 확률 분포에서 샘플링하는 과정에 무작위성을 주입하는 확률적 샘플링(`stochastic sampling`)이 있다. `확률적 샘플링`을 주로 사용한다. `e`가 다음 글자가 될 확률이 0.3이라면, 모델이 `30%` 정도로 이 글자를 선택한다.

모델의 `소프트맥스` 출력은 확률적 샘플링에 사용하기 좋다. 훈련 데이터에는 없지만, 실제 같은 새로운 단어를 만들어 재미있고 창의적으로 보이는 문장을 생성한다.

이때 이 확률 분포의 `엔트로피`를 조절하는 것이 중요하다. 작은 `엔트로피`는 예상 가능한 구조를 가진 `시퀀스`를 생성한다. 즉 더 실제처럼 보인다. 반면 높은 `엔트로피`는 놀랍고 창의적인 `시퀀스`를 만든다. `생성 모델`에서 `샘플링`을 할 때 생성 과정에 무작위성의 양을 바꾸어 시도해 보는 것이 좋다. 흥미는 매우 주관적이므로 최적의 `엔트로피 값`을 미리 알 수 없기 때문이다. 얼마나 흥미로운 데이터를 생성할 것인지는 결국 사람이 판단해야 한다.

`샘플링` 과정에서 확률의 양을 조절하기 위해 소프트맥스 온도(`softmax temperature`)라는 `파라미터`를 사용한다. 이 `파라미터`는 `샘플링`에 사용되는 확률 분포의 `엔트로피`를 나타낸다. 얼마나 놀라운 또는 예상되는 글자를 선택할지 결정한다. `temperature` 값을 주면 다음과 같이 가중치를 적용하여 (모델의 소프트맥스 출력인) 원본 확률 분포에서 새로운 확률 분포를 계산한다.

# 구현

---

## 데이터 전처리

니체의 글을 다운 받고 소문자로 처리한다.

```python
import keras
import numpy as np
path = keras.utils.get_file(
    'nietzsche.txt',
    origin='https://s3.amazonaws.com/text-datasets/nietzsche.txt')
text = open(path).read().lower()
print("size of corpus : ", len(text)) #글의 크기 보기
```

그다음 `maxlen` 길이를 가진 `시퀀스`를 중복하여 추출한다. 추출된 `시퀀스`를 `one-hot` 인코딩으로 변환하고 크기가 (`sequences, maxlen, unique_characteers`)인 `3D` 넘파이 배열 `x`로 합친다. 동시에 훈련 샘플에 상응하는 타깃을 담은 배열 `y`를 준비한다. 타깃은 추출된 `시퀀스` 다음에 오는 `one-hat` 인코딩된 글자이다.

```python
maxlen = 60
step = 3

sentences = []

next_chars = []

for i in range(0, len(text) - maxlen, step):
    sentences.append(text[i: i + maxlen])
    next_chars.append(text[i+maxlen])
    
print ('num of sequence : ', len(sentences))
    
chars = sorted(list(set(text)))
print('unique char : ', len(chars))
char_indices = dict((char, chars.index(char)) for char in chars)
    
print("vectorization...")
x = np.zeros((len(sentences), maxlen, len(chars)), dtype=np.bool)
y = np.zeros((len(sentences), len(chars)), dtype = np.bool)
for i, sentence in enumerate(sentences):
    for t, char in enumerate(sentence):
        x[i, t, char_indices[char]]=1
    y[i, char_indices[next_chars[i]]] = 1
```

## 네트워크 구성

이 네트워크는 하나의 `LSTM` 층과 그 뒤에 `Dense` 분류기가 뒤따른다. 분류기는 가능한 모든 글자에 대한 `소프트맥스` 출력을 만든다. `순환 신경망`이 `시퀀스` 데이터를 생성하는 유일한 방법은 아니다. 최근에는 `1D 컨브넷`도 이런 작업에 아주 잘 들어맞는다는 것이 밝혀졌다.

```python
from keras import layers
model = keras.models.Sequential()
model.add(layers.LSTM(128, input_shape = (maxlen, len(chars))))
model.add(layers.Dense(len(chars), activation='softmax'))
```

타깃이 `ont-hat` 인코딩되어 있기 때문에 모델을 훈련하기 위해 `categorial_crossentropy`를 사용한다

```python
optimizer = keras.optimizers.RMSprop(lr=0.01)
model.compile(loss='categorical_crossentropy', optimizer=optimizer)
```

## 언어 모델 훈련과 샘플링

훈련된 모델과 `seed`로 쓰일 간단한 텍스트를 주면 다음과 같이 반복하여 새로운 텍스트를 생성할 수 있다.

1. 지금까지 생성된 텍스트를 주입하여 모델에서 다음 글자에 대한 확률 분포를 뽑기
2. 특정 온도로 이 확률 분포에 가중치 조정
3. 가중치가 조정된 분포에서 무작위로 새로운 글자 샘플링
4. 새로운 글자를 생성된 텍스트의 끝에 추가

다음은 모델에서 나온 원본 확률 분포에 가중치를 조정하고 새로운 글자의 인덱스를 추출한다(`셈플링` 함수이다).

### 샘플링 함수
```python
def sample(preds, temperature=1.0):
    preds = np.asarray(preds).astype('float64')
    preds = np.log(preds) / temperature
    exp_preds = np.exp(preds)
    preds = exp_preds / np.sum(exp_preds)
    probas = np.random.multinomial(1, preds, 1)
    return np.argmax(probas)
```

마지막으로 다음 반복문은 반복적으로 훈련하고 텍스트를 생성한다. `에포크`마다 학습이 끝난 후 여러 가지 온도를 사용하여 텍스트를 생성한다. 이렇게 하면 `모델`이 수렴하면서 생성된 텍스트가 어떻게 진화하는지 볼 수 있다. 온도가 `샘플링` 전략에 미치는 영향도 보여준다.

### 텍스트 생성
```python
import random
import sys

random.seed(42)
start_index = random.randint(0, len(text) - maxlen - 1)

for epoch in range(1, 60):
    print("epoch", epoch)
    model.fit(x, y, batch_size=128, epochs=1)
    
    seed_text = text[start_index: start_index + maxlen]
    print('--- seed text : "' + seed_text + '"')
    
    for temperature in [0.2, 0.5, 1.0, 1.2]:
        print('------temperature : ', temperature)
        generated_text = seed_text
        sys.stdout.write(generated_text)
        
        for i in range(400):
            sampled = np.zeros((1, maxlen, len(chars)))
            for t, char in enumerate(generated_text):
                sampled[0, t, char_indices[char]] = 1.
                
            preds = model.predict(sampled, verbose=0)[0]
            next_index = sample(preds, temperature)
            next_char = chars[next_index]
            
            generated_text += next_char
            generated_text = generated_text[1:]
            
            sys.stdout.write(next_char)
            sys.stdout.flush()
        print()
```

seed text는 다음으로 정의한다. -> "the slowly ascending ranks and classes, in which,
through fo"

### epoch 7에서의 결과
```
epoch 7
Epoch 1/1
200278/200278 [==============================] - 436s 2ms/step - loss: 1.4196
--- seed text : "the slowly ascending ranks and classes, in which,
through fo"
------temperature :  0.2
the slowly ascending ranks and classes, in which,
through for the sense of the conduct of the spirit of the same the standard and and say, and the end the same and the same as the same as the subling of the spirit of the spirit of the same and are such a souls and soul and the same and the same as the manifestated the same and and the same as the same and souls to the standard and substiment of the sentiment of the same as the struction of the spirit of in
------temperature :  0.5
the slowly ascending ranks and classes, in which,
through for it is a german not only his ascertains
that it is also the compare the course to much of the general one of the standard; the oursely with one scorns of the general decises to the enlude, that something such a moral that is also the contraditian and dishangained and in a sympathy and and strange of belief of the indignation of moral counter soul, and moral all know socief to the opposite the com
------temperature :  1.0
the slowly ascending ranks and classes, in which,
through forse--ground it through forwaugus? theref aths to the power--to ancums of wimate, heresely to veretwheness,
in itraile must dodings, overstoly as little also one have different and iwse thars
opposed world hench
his idearing a life of the
something in ages upuribies, of the
reason
believes ever peoplener of hont
of
reader divine, the erork, and dehin from superoint
as simpleptation of hruth--wis wi
------temperature :  1.2
the slowly ascending ranks and classes, in which,
through for enclushating thank entlackesk and requiteh of preisvalariantk while discorsfine, that to hard, and tekip rround." but flover kibfine
havingued again vulgarial arise--in the vivest, genius om, that blengk;ritage hysor caceju:, is all philosophinalge, his sec spainhild, o.
even have way, likilr, twarevanneden
they. cocise
and we undners-solisting me-primitive--periodoue ieadius on posscjut to outf
```
## 결론

생각보다 간단한 방법으로 샘플링을 하여 텍스트 생성을 할 수 있다.