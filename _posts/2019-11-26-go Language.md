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
#### 포인터연산자
```
var k int = 10
var p = &k  //k의 주소를 할당
println(*p) //p가 가리키는 주소에 있는 실제 내용을 출력
```

#### for range 문
```
names := []string{"홍길동", "이순신", "강감찬"}
for index, name := range names {
    println(index, name)
}
```

#### break, continue, goto 문
- for 루프를 빠져나와 L1 레이블로 이동한 후, break가 있는 현재 for 루프를 건너뛰고 다음 문장인 println() 으로 이동

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

#### Variadic Function 가변인자함수
- 문자열 가변 파라미터를 나타내기 위해서 ...string 과 같이 표현

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

#### 함수 리턴값
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

#### 익명함수
- 함수명을 갖지 않는 함수를 익명함수(Anonymous Function)

#### 일급함수
- Go 프로그래밍 언어에서 함수는 일급함수로서 Go의 기본 타입과 동일하게 취급되며, 따라서 다른 함수의 파라미터로 전달하거나 다른 함수의 리턴값으로도 사용될 수 있다

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

####  type문을 사용한 함수 원형 정의
- 이렇게 함수의 원형을 정의하고 함수를 타 메서드에 전달하고 리턴받는 기능을 타 언어에서 흔히 델리게이트(Delegate)라 부른다. Go는 이러한 Delegate 기능을 제공하고 있다

```
// 원형 정의
type calculator func(int, int) int
 
// calculator 원형 사용
func calc(f calculator, a int, b int) int {
    result := f(a, b)
    return result
}
```

#### 클로저 (Closure)
- Go 언어에서 함수는 Closure로서 사용될 수도 있다. Closure는 함수 바깥에 있는 변수를 참조하는 함수값(function value)를 일컫는데, 이때의 함수는 바깥의 변수를 마치 함수 안으로 끌어들인 듯이 그 변수를 읽거나 쓸 수 있게 된다.

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
#### 슬라이스(Slice)
- 슬라이스의 길이(Length)와 용량(Capacity)
```
func main() {
    s := make([]int, 5, 10)
    println(len(s), cap(s)) // len 5, cap 10
}

슬라이스에 별도의 길이와 용량을 지정하지 않으면, 기본적으로 길이와 용량이 0 인 슬라이스를 만드는데, 이를 Nil Slice 라 하고, nil 과 비교하면 참을 리턴한다.

func main() {
    var s []int
 
    if s == nil {
        println("Nil Slice")
    }
    println(len(s), cap(s)) // 모두 0
}
```

- 부분 슬라이스(Sub-slice)
```
s := []int{0, 1, 2, 3, 4, 5}
s = s[2:5]     // 2, 3, 4
s = s[1:]      // 3, 4
fmt.Println(s) // 3, 4 출력
```

- 슬라이스 추가,병합(append)과 복사(copy)
```
package main
 
import "fmt"
 
func main() {
    // len=0, cap=3 인 슬라이스
    sliceA := make([]int, 0, 3)
 
    // 계속 한 요소씩 추가
    for i := 1; i <= 15; i++ {
        sliceA = append(sliceA, i)
        // 슬라이스 길이와 용량 확인
        fmt.Println(len(sliceA), cap(sliceA))
    }
 
    fmt.Println(sliceA) // 1 부터 15 까지 숫자 출력 
}

func main() {
    source := []int{0, 1, 2}
    target := make([]int, len(source), cap(source)*2)
    copy(target, source)
    fmt.Println(target)  // [0 1 2 ] 출력
    println(len(target), cap(target)) // 3, 6 출력
}
```

#### Map 개요
```
tickers := map[string]string{
    "GOOG": "Google Inc",
    "MSFT": "Microsoft",
    "FB":   "FaceBook",
}

package main
 
func main() {
    tickers := map[string]string{
        "GOOG": "Google Inc",
        "MSFT": "Microsoft",
        "FB":   "FaceBook",
        "AMZN": "Amazon",
    }
 
    // map 키 체크
    val, exists := tickers["MSFT"]
    if !exists {
        println("No MSFT ticker")
    }

    for key, val := range tickers {
        fmt.Println(key, val)
    }    
}

```

#### 패키지 Scope
- 패키지 내에는 함수, 구조체, 인터페이스, 메서드 등이 존재하는데, 이들의 이름(Identifier)이 첫문자를 대문자로 시작하면 이는 public 으로 사용할 수 있다. 즉, 패키지 외부에서 이들을 호출하거나 사용할 수 있게 된다. 반면, 이름이 소문자로 시작하면 이는 non-public 으로 패키지 내부에서만 사용될 수 있다.

#### 패키지 init 함수와 alias
```
package testlib
 
var pop map[string]string
 
func init() {   // 패키지 로드시 map 초기화
    pop = make(map[string]string)
}

package main
import _ "other/xlib" //그 패키지 안의 init() 함수만을 호출하고자 하는 케이스

// 패키지 alias를 사용해서 구분
import (
    mongo "other/mongo/db"
    mysql "other/mysql/db"
)
func main() {
    mondb := mongo.Get()
    mydb := mysql.Get()
    //...
}
```

#### Struct (구조체)
```
package main
 
import "fmt"
 
// struct 정의
type person struct {
    name string
    age  int
}
 
func main() {
    // person 객체 생성
    p := person{}
     
    // 필드값 설정
    p.name = "Lee"
    p.age = 10
     
    fmt.Println(p)
}
```

#### Go 메서드(Method)
```
package main
 
//Rect - struct 정의
type Rect struct {
    width, height int
}
 
//Rect의 area() 메소드
func (r Rect) area() int {
    return r.width * r.height   
}
 
func main() {
    rect := Rect{10, 20}
    area := rect.area() //메서드 호출
    println(area)
}
```

#### Go 인터페이스
```
type Shape interface {
    area() float64
    perimeter() float64
}


//Rect 정의
type Rect struct {
    width, height float64
}
 
//Circle 정의
type Circle struct {
    radius float64
}
 
//Rect 타입에 대한 Shape 인터페이스 구현 
func (r Rect) area() float64 { return r.width * r.height }
func (r Rect) perimeter() float64 {
     return 2 * (r.width + r.height)
}
 
//Circle 타입에 대한 Shape 인터페이스 구현 
func (c Circle) area() float64 { 
    return math.Pi * c.radius * c.radius
}
func (c Circle) perimeter() float64 { 
    return 2 * math.Pi * c.radius
}

```

#### 인터페이스 타입
-- 빈 interface는 interface{} 와 같이 표현한다.

```
func Marshal(v interface{}) ([]byte, error);
 
func Println(a ...interface{}) (n int, err error);
 인터페이스는 어떠한 타입도 담을 수 있는 컨테이너라고 볼 수 있으며, 여러 다른 언어에서 흔히 일컫는 Dynamic Type 이라고 볼 수 있다. (주: empty interface는 C#, Java 에서 object라 볼 수 있으며, C/C++ 에서는 void* 와 같다고 볼 수 있다)
```

-- Type Assertion
```
Interface type의 x와 타입 T에 대하여 x.(T)로 표현했을 때, 이는 x가 nil이 아니며, x는 T 타입에 속한다는 점을 확인(assert)하는 것으로 이러한 표현을 "Type Assertion"이라 부른다.

func main() {
    var a interface{} = 1
 
    i := a       // a와 i 는 dynamic type, 값은 1
    j := a.(int) // j는 int 타입, 값은 1
 
    println(i)  // 포인터주소 출력
    println(j)  // 1 출력
}
```

#### Go 에러
- Go는 내장 타입으로 error 라는 interface 타입을 갖는다

```
type error interface {
    Error() string
}
```

- Go 함수가 결과와 에러를 함께 리턴한다면, 이 에러가 nil 인지를 체크해서 에러가 없는지를 체크할 수 있다

```
package main
 
import (
    "log"
    "os"
)
 
func main() {
    f, err := os.Open("C:\\temp\\1.txt")
    if err != nil {
        log.Fatal(err.Error())
    }
    println(f.Name())
}
```

-- error의 Type을 체크해서 에러 타입별로 별도의 에러 처리를 하는 방식
```
_, err := otherFunc()
switch err.(type) {
default: // no error
    println("ok")
case MyError:
    log.Print("Log my error")
case error:
    log.Fatal(err.Error())
}
```

#### 지연실행 defer
- 차후 문장에서 어떤 에러가 발생하더라도 항상 파일을 Close할 수 있도록 한다.
```
package main
 
import "os"
 
func main() {
    f, err := os.Open("1.txt")
    if err != nil {
        panic(err)
    }
 
    // main 마지막에 파일 close 실행
    defer f.Close()
 
    // 파일 읽기
    bytes := make([]byte, 1024)
    f.Read(bytes)
    println(len(bytes))
}
```

#### panic 함수
- Go 내장함수인 panic()함수는 현재 함수를 즉시 멈추고 현재 함수에 defer 함수들을 모두 실행한 후 즉시 리턴한다.
```
package main
 
import "os"
 
func main() {
    openFile("Invalid.txt")
    println("Done") //이 문장은 실행 안됨
}
 
func openFile(fn string) {
    f, err := os.Open(fn)
    if err != nil {
        panic(err)
    }
    // 파일 close 실행됨
    defer f.Close()
}
```

#### recover 함수
- Go 내장함수인 recover()함수는 panic 함수에 의한 패닉상태를 다시 정상상태로 되돌리는 함수이다
```
package main
 
import (
    "fmt"
    "os"
)
 
func main() {
    openFile("1.txt")
    println("Done") // 이 문장 실행됨
}
 
func openFile(fn string) {
    // defere 함수. panic 호출시 실행됨
    defer func() {
        if r := recover(); r != nil {
            fmt.Println("OPEN ERROR", r)
        }
    }()
 
    f, err := os.Open(fn)
    if err != nil {
        panic(err)
    }
 
    // 파일 close 실행됨
    defer f.Close()
}
```

#### Go루틴
- Go루틴(goroutine)은 Go 런타임이 관리하는 Lightweight 논리적 (혹은 가상적) 쓰레드
```
goroutine은 OS 쓰레드보다 훨씬 가볍게 비동기 Concurrent 처리를 구현하기 위하여 만든 것으로, 기본적으로 Go 런타임이 자체 관리한다. Go 런타임 상에서 관리되는 작업단위인 여러 goroutine들은 종종 하나의 OS 쓰레드 1개로도 실행되곤 한다. 즉, Go루틴들은 OS 쓰레드와 1 대 1로 대응되지 않고, Multiplexing으로 훨씬 적은 OS 쓰레드를 사용한다. 메모리 측면에서도 OS 쓰레드가 1 메가바이트의 스택을 갖는 반면, goroutine은 이보다 훨씬 작은 몇 킬로바이트의 스택을 갖는다(필요시 동적으로 증가). Go 런타임은 Go루틴을 관리하면서 Go 채널을 통해 Go루틴 간의 통신을 쉽게 할 수 있도록 하였다.
```