---
layout: post
title: "Python develop language"
description: 
headline: 
modified: 2019-12-04
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


## 주요 기능
### if __name__ == '__main__' 의미
- __name__ 은 현재 모듈의 이름을 담고 있는 내장 변수다.

- 해당 프로그램을 직접 실행했을 경우에는 참이 되어 main() 함수를 실행하고, 다른 프로그램에서 import하여 사용할 경우에는 간접 실행이 되어 거짓이 되어  main()함수가 실행되지 않는다.

- 다른 모듈을 import하는 경우는 main안의 코드를 실행하기 보다, 함수나 클래스등만을 사용하는 경우가 대부분.  if __name__ == '__main__'  을 사용하여 코드의 수정없이 바로 import하여 사용 가능.

- 메인 프로그램으로 실행하기 위해 설정.
다른 모듈에 의해 사용된다면 그 모듈 이름이 새겨짐.

- 예를 들어  __name__  이 있는 파일이 aaa.py라면 __name__ 변수에는 __main__ 이라는 값이 들어감.
하지만 aaa.py를 외부에서 import하여 실행하면 __name__ 에는 파일이름 aaa가 들어감.

-  => 요약하자면 해당 모듈이 직접 실행되는 경우에는 __name__ 은 __main__ 으로 설정되어 if문 아래를 실행하지만, 외부에서 실행된 경우에는 __name__ 이 __main__이 아니기 때문에 if문 아래를 실행하지 않는다.

### 스레드(Thread)
- 1개의 프로세스(컴퓨터에서 동작하고 있는 프로그램)는 한가지 일을 하지만, 스레드를 이용하여 2가지 이상의 일을 동시에 수행할 수 있다.

- 예를 들어 실시간 채팅을 하는 코드를 만들 때, 송신하는 코드와 수신하는 코드를 별개로 작동시킬 수 있다.

- threading 모듈 이용. import threading
threading에서 내장 모듈인 Thread를 상속받음.

- threading.Thread 클래스를 상속받는 클래스를 만들어서 run() 하여 객체 생성
★★ Thread를 구동하기 위해서는 함수명을 run으로 해야함
​	MyThread로 생성된 객체를 start() 메소드를 실행할 때 run 메소드가 자동으로 수행.

- thread 객체 생성 후 start() 메소드를 통해 thread 객체 실행
- target은 스레드로 돌릴 함수, args는 입력 인자.
- join() 메소드를 통해 스레드가 끝날 때까지 기다림

### 단위 테스트 프레임워크(unittest)

'''
import unittest

class TestStringMethods(unittest.TestCase):

    def test_upper(self):
        self.assertEqual('foo'.upper(), 'FOO')

    def test_isupper(self):
        self.assertTrue('FOO'.isupper())
        self.assertFalse('Foo'.isupper())

    def test_split(self):
        s = 'hello world'
        self.assertEqual(s.split(), ['hello', 'world'])
        # check that s.split fails when the separator is not a string
        with self.assertRaises(TypeError):
            s.split(2)

if __name__ == '__main__':
    unittest.main()
'''

- python -m unittest tests/test_something.py
- python -m unittest -v tests/test_something.py


### yield 
#### 이터러블(Iterables)
- 메모리에 담아 사용

'''
mylist = [x * x for x in range(3)]
for i in mylist:
    print(i)
0
1
4
'''

#### 제너레이터(Generators)
- 메모리에 담고 있지 않고 그때그때 값을 생성(generator)해서 반환
- [] 대신 ()를 사용
- for i in mygenerator 코드를 두 번 실행할 수는 없습니다. 제너레이터는 한 번만 사용될 수 있기 때문입니다: 제너레이터는 0을 계산해서 반환한 후 0에 대해서는 아예 잊습니다, 그리고 1을 계산하고 한 번에 하나씩 처리해가며 순환을 종료

'''
>>> mygenerator = (x * x for x in range(3))
>>> for i in mygenerator:
...    print(i)
0
1
4
'''

#### Yield
- 함수로부터 만들어진 제너레이터 객체가 for 루프를 통해 처음 실행될 때 Python은 함수 내에 있는 코드를 yield 키워드를 만나기 전까지 실행하고 첫 번째 루프의 값을 반환하게 됩니다. 다음 루프 때에는 yield 키워드 뒤에 있는 코드를 실행하고 다시 루프를 돌면서 반환할 값이 아예 없을 때까지 계속 같은 과정을 반복하게 됩니다.

'''
def number_generator():
    yield 0
    yield 1
    yield 2
 
for i in number_generator():
    print(i)

0
1
2    
'''

'''
def createGenerator():
    mylist = range(3)
    for i in mylist:
        yield i * i

mygenerator = createGenerator() # 제너레이터 생성
print(mygenerator) # mygenerator는 객체입니다.
<generator object createGenerator at 0xb7555c34>
for i in mygenerator:
    print(i)

0
1
4
'''

'''
def one_generator():
    yield 1
    return 'return에 지정한 값'
 
try:
    g = one_generator()
    next(g)
    next(g)
except StopIteration as e:
    print(e)    # return에 지정한 값

>>> return에 지정한 값
'''

'''
>>> class Bank(): # 은행을 만들고 ATM도 만듭시다.
...    crisis = False
...    def create_atm(self):
...        while not self.crisis:
...            yield "$100"
>>> hsbc = Bank() # 아무 문제 없다면 ATM은 원하는 만큼 줄겁니다.
>>> corner_street_atm = hsbc.create_atm()
>>> print(corner_street_atm.next())
$100
>>> print(corner_street_atm.next())
$100
>>> print([corner_street_atm.next() for cash in range(5)])
['$100', '$100', '$100', '$100', '$100']
>>> hsbc.crisis = True # 경제 공황이 오고 있습니다, 돈이 더 없겠네요!
>>> print(corner_street_atm.next())
<type 'exceptions.StopIteration'>
>>> wall_street_atm = hsbc.create_atm() # 새로운 ATM을 만들어도 마찬가지입니다.
>>> print(wall_street_atm.next())
<type 'exceptions.StopIteration'>
>>> hsbc.crisis = False # 경제 공황이 끝났음에도 ATM은 모두 비어있습니다.
>>> print(corner_street_atm.next())
<type 'exceptions.StopIteration'>
>>> brand_new_atm = hsbc.create_atm() # 다시 일상으로 돌아가기 위해 새로운 ATM을 만듭니다.
>>> for cash in brand_new_atm:
...    print(cash)
$100
$100
$100
$100
$100
$100
$100
$100
$100
'''