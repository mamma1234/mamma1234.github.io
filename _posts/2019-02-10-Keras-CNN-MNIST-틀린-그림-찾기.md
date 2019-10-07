---
layout: post
title: "Keras CNN MNIST 틀린 그림 찾기"
description: 
headline: 
modified: 2019-02-10
category: Keras
tags: [Keras, CNN, MNIST, 대화 내용 분석]
imagefeature: 
mathjax: 
chart: 
share: true
comments: true
---

Keras로 간단한 [CNN을 구현](https://github.com/newhiwoong/Keras-Applications/blob/master/01_CNN_MNIST.ipynb)하여 MNIST를 진행하면 99% 이상의 성능을 발휘한다. 그럼 1% 미만이 틀린 MNIST는 어떤 그림일지 궁금했고 한 번 알아보려고 한다.

[나의 Github](https://github.com/newhiwoong)에 [Keras-Applications](https://github.com/newhiwoong/Keras-Applications)에서 [전체 코드](https://github.com/newhiwoong/Keras-Applications/blob/master/01_CNN_MNIST.ipynb)를 볼 수 있다.

## Keras CNN MNIST 

우선 모델을 만드는데 필요한 라이브러리들을 `import` 한다.
```python
from keras import layers
from keras import models
```

그리고 간단한 모델을 제작한다.
```python
model = models.Sequential()
model.add(layers.Conv2D(32, (3,3),activation='relu', input_shape = (28,28,1)))
model.add(layers.MaxPool2D((2,2)))
model.add(layers.Conv2D(64, (3,3), activation='relu'))
model.add(layers.MaxPooling2D(2,2))
model.add(layers.Conv2D(64, (3,3), activation='relu'))
model.add(layers.Flatten())
model.add(layers.Dense(64, activation='relu'))
model.add(layers.Dense(10, activation='softmax'))
```

![]({{ site.url }}/images/Keras_CNN_MNIST1.JPG)  
모델의 구조

평가할 `MNIST`를 받고 
```python
from keras.datasets import mnist
from keras.utils import to_categorical
(train_images, train_labels), (test_images, test_labels) = mnist.load_data()
```

사용할 수 있게 `전처리`를 진행한다.
```python
train_images = train_images.reshape((60000, 28, 28, 1))
train_images = train_images.astype('float32') / 255

test_images = test_images.reshape((10000, 28, 28 ,1))
test_images = test_images.astype('float32') / 255

train_labels = to_categorical(train_labels)
test_labels = to_categorical(test_labels)
```

이제 위에서 만든 모델을 `training`하고
```python
model.compile(optimizer='rmsprop',
              loss='categorical_crossentropy',
              metrics=['accuracy'])
model.fit(train_images, train_labels, epochs=5, batch_size=64)
```

![]({{ site.url }}/images/Keras_CNN_MNIST2.JPG)  
`test_loss, test_acc = model.evaluate(test_images, test_labels)`

99.14%로 매우 높은 성능을 자랑한다.

## MNIST 시각화
필요한 라이브러리들을 `import` 한다.
```python
import random
import matplotlib.pyplot as plt
```

그리고 손글씨 이미지와 예상되는 정답 값, 실제 정답 값을 10개 출력해본다.
```python
for i in range(10):
    r = random.randint(0, len(test_images) -1)

    digit = test_images[r].reshape((28, 28))
    digit = digit.astype('float32') * 255
    digit = digit.astype('uint8')
    digit

    plt.imshow(digit, cmap=plt.cm.binary)
    plt.show()
    print("예상 정답값 : ",int(model.predict_classes(test_images[r].reshape((1, 28, 28, 1)))))
    print("실제 정답값 : ",list(test_labels[r]).index(1.0))

```

![]({{ site.url }}/images/Keras_CNN_MNIST3.JPG)  
나도 알아보기 힘들 사진들도 인식한다.

10개로는 부족하니 1000개 중에서 예상값과 정답값이 다른 이미지만 출력하게 한다.
```python
for i in range(1000):
    r = random.randint(0, len(test_images) -1)
    if int(model.predict_classes(test_images[r].reshape((1, 28, 28, 1)))) != list(test_labels[r]).index(1.0):
        digit = test_images[r].reshape((28, 28))
        digit = digit.astype('float32') * 255
        digit = digit.astype('uint8')
        digit

        plt.imshow(digit, cmap=plt.cm.binary)
        plt.show()
        print("예상 정답값 : ",int(model.predict_classes(test_images[r].reshape((1, 28, 28, 1)))))
        print("실제 정답값 : ",list(test_labels[r]).index(1.0))
```

![]({{ site.url }}/images/Keras_CNN_MNIST4.JPG)  
틀린 이미지들이 보인다.

### 결론

컴퓨터의 한계로 글씨가 뭉개지거나 중간에 끊긴 부분이 있는 이미지들을 제대로 인식하지 못하는 경향이 보이는 거 같다.
