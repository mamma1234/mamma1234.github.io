---
layout: post
title: "GO google develop language"
description: 
headline: 
modified: 2019-11-26
category: development
imagefeature: cover3.jpg
tags: [Go]
mathjax: 
chart: 
share: true
comments: true
featured: true
disqus:
---

# Record
## 개념
- Go는 전통적인 컴파일, 링크 모델을 따르는 범용 프로그래밍 언어이다. Go는 일차적으로 시스템 프로그래밍을 위해 개발되었으며, C++, Java, Python의 장점들을 뽑아 만들어졌다. C++와 같이 Go는 컴파일러를 통해 컴파일되며, 정적 타입 (Statically Typed)의 언어이다. 또한 Java와 같이 Go는 Garbage Collection 기능을 제공한다. Go는 단순하고 간결한 프로그래밍 언어를 지향하였는데, Java의 절반에 해당하는 25개의 키워드만으로 프로그래밍이 가능하게 하였다. 마지막으로 Go의 큰 특징으로 Go는 Communicating Sequential Processes (CSP) 스타일의 Concurrent 프로그래밍을 지원한다.

## 환경변수
### GOROOT
- Go가 설치된 디렉토리(윈도우즈의 경우 디폴트로 C:\Go)를 가리키며, Go 실행파일은 GOROOT/bin 폴더에, Go 표준 패키지들은 GOROOT/pkg 폴더에 있다. (윈도우즈에 GO 설치시 시스템 환경변수로 자동으로 설정된다)

### GOPATH
- Go는 표준 패키지 이외의 3rd Party 패키지나 사용자 정의 패키지들을 이 GOPATH 에서 찾는다. 복수 개의 경로를 지정한 경우, 3rd Party 패키지는 처음 경로에 설치된다.

### 주요 명령어
go run src/hello.go
go build test.go

### 주요 문법
- 포인터연산자
```
var k int = 10
var p = &k  //k의 주소를 할당
println(*p) //p가 가리키는 주소에 있는 실제 내용을 출력
```

- for range 문
```
names := []string{"홍길동", "이순신", "강감찬"}
for index, name := range names {
    println(index, name)
}
```

- break, continue, goto 문
for 루프를 빠져나와 L1 레이블로 이동한 후, break가 있는 현재 for 루프를 건너뛰고 다음 문장인 println() 으로 이동
```
package main

func main() {
    i := 0
 
L1:
    for {
     
        if i == 0 {
            break L1
        }
    }
 
    println("OK")
}
```

- Variadic Function 가변인자함수
문자열 가변 파라미터를 나타내기 위해서 ...string 과 같이 표현
```
package main
func main() {   
    say("This", "is", "a", "book")
    say("Hi")
}
 
func say(msg ...string) {
    for _, s := range msg {
        println(s)
    }
}
```

- 함수 리턴값
```
package main
 
func main() {
    count, total := sum(1, 7, 3, 5, 9)
    println(count, total)   
}

//리턴값 복수
func sum(nums ...int) (int, int) {
    s := 0      // 합계
    count := 0  // 요소 갯수
    for _, n := range nums {
        s += n
        count++
    }
    return count, s
}

// Named Return Parameter = count int, total int
func sum(nums ...int) (count int, total int) {
    for _, n := range nums {
        total += n
    }
    count = len(nums)
    return
}
```

- 익명함수
함수명을 갖지 않는 함수를 익명함수(Anonymous Function)

- 일급함수
Go 프로그래밍 언어에서 함수는 일급함수로서 Go의 기본 타입과 동일하게 취급되며, 따라서 다른 함수의 파라미터로 전달하거나 다른 함수의 리턴값으로도 사용될 수 있다
```
package main
 
func main() {
    //변수 add 에 익명함수 할당
    add := func(i int, j int) int {
        return i + j
    }
 
    // add 함수 전달
    r1 := calc(add, 10, 20)
    println(r1)
 
    // 직접 첫번째 파라미터에 익명함수를 정의함
    r2 := calc(func(x int, y int) int { return x - y }, 10, 20)
    println(r2)
 
}
 
func calc(f func(int, int) int, a int, b int) int {
    result := f(a, b)
    return result
}
```

-  type문을 사용한 함수 원형 정의
이렇게 함수의 원형을 정의하고 함수를 타 메서드에 전달하고 리턴받는 기능을 타 언어에서 흔히 델리게이트(Delegate)라 부른다. Go는 이러한 Delegate 기능을 제공하고 있다
```
// 원형 정의
type calculator func(int, int) int
 
// calculator 원형 사용
func calc(f calculator, a int, b int) int {
    result := f(a, b)
    return result
}
```

- 클로저 (Closure)
Go 언어에서 함수는 Closure로서 사용될 수도 있다. Closure는 함수 바깥에 있는 변수를 참조하는 함수값(function value)를 일컫는데, 이때의 함수는 바깥의 변수를 마치 함수 안으로 끌어들인 듯이 그 변수를 읽거나 쓸 수 있게 된다.
```
package main
 
func nextValue() func() int {
    i := 0
    return func() int {
        i++
        return i
    }
}
 
func main() {
    next := nextValue()
 
    println(next())  // 1
    println(next())  // 2
    println(next())  // 3
 
    anotherNext := nextValue()
    println(anotherNext()) // 1 다시 시작
    println(anotherNext()) // 2
}
```