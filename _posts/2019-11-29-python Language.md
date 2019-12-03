---
layout: post
title: "Python develop language"
description: 
headline: 
modified: 2019-11-29
category: development
imagefeature: cover3.jpg
tags: [Python]
mathjax: 
chart: 
share: true
comments: true
featured: true
disqus:
---

# Record
## 개념
- 
## 주요 명령어


## 주요 문법
### None
- 이 형은 하나의 값만을 갖습니다. 이 값을 갖는 하나의 객체가 존재합니다. 이 객체에는 내장된 이름 None 을 통해 접근합니다. 여러 가지 상황에서 값의 부재를 알리는 데 사용됩니다. 예를 들어, 명시적으로 뭔가를 돌려주지 않는 함수의 반환 값입니다. 논리값은 거짓입니다.

```
<class 'NoneType'>
```

### snake case
- 뱀 같은 표기법 _
- a_none, a_study

### Lists
- 리스트의 항목은 임의의 파이썬 객체입니다. 리스트는 콤마로 분리된 표현식을 대괄호 안에 넣어서 만들 수 있습니다. (길이 0이나 1의 리스트를 만드는데 별도의 규칙이 필요 없습니다.)

```
["mon","tue","wed","thur","fri"]
<class 'list'>
```


### Tuples
- 튜플의 항목은 임의의 파이썬 객체입니다. 두 개 이상의 항목으로 구성되는 튜플은 콤마로 분리된 표현식의 목록으로 만들 수 있습니다. 하나의 항목으로 구성된 튜플(싱글턴,singleton)은 표현식에 콤마를 붙여서 만들 수 있습니다(괄호로 표현식을 묶을 수 있으므로, 표현식 만으로는 튜플을 만들지 않습니다). 빈 튜플은 한 쌍의 빈 괄호로 만들 수 있습니다.

```
("mon","tue","wed","thur","fri")
<class 'tuple'>
```


### Dictionary

```
{'jack': 4098, 'sape': 4139}
<class 'dict'>
```

### Function
#### Builtin Function
```
print(type(print))
<class 'builtin_function_or_method'>
```

#### define Function
```
def say_hello():
  print("hello")
<class 'function'>
```

#### Function Arguments
```
def minus(a, b=0)
  print(a-b)
minus(2)
```

#### Function Keyworded Arguments
```
def plus(a, b):
  return a-b
result = plus(b=30, a=1)
print(result)   

-20


def plus(a, b, *args, **kwargs):
  print(args)
  print(kwargs)
  return a+b
result = plus(1,2,12,312,3,4,123,hello1=True,hello2=True,hello3=True,hello4=True,)
print(result)

(12, 312, 3, 4, 123)
{'hello1': True, 'hello2': True, 'hello3': True, 'hello4': True}
3
```

#### if, elif, else
```
if age < 18:
    print(age)
elif age == 18:
    print(age)
else:
    print("out")
```

#### for in
```
for day in ["1", "2", "3", "4", "5"]:
  print(day)
```

#### break, continue, else
```
for n in range(2, 10):
     for x in range(2, n):
         if n % x == 0:
             print(n, 'equals', x, '*', n//x)
             break
     else:
         # loop fell through without finding a factor
         print(n, 'is a prime number')

2 is a prime number
3 is a prime number
4 equals 2 * 2
5 is a prime number
6 equals 2 * 3
7 is a prime number
8 equals 2 * 4
9 equals 3 * 3

for num in range(2, 10):
     if num % 2 == 0:
         print("Found an even number", num)
         continue
     print("Found a number", num)
Found an even number 2
Found a number 3
Found an even number 4
Found a number 5
Found an even number 6
Found a number 7
Found an even number 8
Found a number 9
```

#### module
```
import math
print(math.ceil(1.2))

from math import ceil
print(ceil(1.2))
```