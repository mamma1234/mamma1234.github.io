---
layout: post
title: "Kotlin"
description: 
headline: 
modified: 2020-02-29
category: webdevelopment
imagefeature: cover3.jpg
tags: [Kotlin]
mathjax: 
chart: 
share: true
comments: true
featured: false
disqus:
---
# Kotlin

## 개요
Kotlin언어란 IntelliJ IDEA 소프트웨어를 제작한 JetBrain사가 2011년 제작한 프로그래밍 언어
[https://try.kotlinlang.org] (https://try.kotlinlang.org)

## 특징
JVM에서 동작하는 Kotlin언어는 Java언어와 100% 호환이 가능
Java언어로 작성된 스크립트를 Kotlin언어로 바꾸는 기능


## Nullable
```JavaScript
    fun strlen (s: String?) = s.length() 

    Nullable

    fun strlen (s: String?) : Int =
        if (s != null) s.length() else 0

```

## 함수와 변수
- fun 함수
```JavaScript
    fun sum(a: Int, b: Int) : Int {
        return a+b
    }

    fun sum(a: Int, b: Int) : Int = a+b
```

- 타입 추론 (Type Inference)
```JavaScript
    fun sum(a: Int, b: Int) = a+b
```

- 디폴트 값
```JavaScript
    fun sum(a: Int, b: Int = 10) = a+b

    fun main(args: Array<String>){
        println(sum(1))
    }

    $ 11
```

- var, val 변수 선언
```JavaScript
    변경 가능한 변수 var
    변경 불가능한 변수 val
```
```JavaScript
    var name: String
    var age: Int = 20
```

- 변수 타입 추론
```JavaScript
    var name = "Mongue"
```

## 클래스
- class
```JavaScript
    class Button {
        var id: Int = 0
    }

```

- 객체 생성시 new 사용하지 않음
```JavaScript
    val button = Button()
```

- 가시성 변경자 (Visibility Modifier)
```JavaScript
    public:     클래스 (모든곳),            최상위함수/변수 (모든곳)
    internal:   클래스 (같은 모듈내),       최상위함수/변수 (같은 모듈내)
    protected:  클래스 (하위 클래스 내),    최상위함수/변수 (사용 불가)
    private:    클래스 (같은 클래스 내),    최상위함수/변수 (같은 파일내)

```


## 클래스의 생성자 (Constructor)
- 주생성자 (Primary Constructor)
```JavaScript
    // 주 생성자 생략
    class Button {
        var id: Int =0
    }

    // 매개변수가 없는 주 생성자 생략
    class Button(){
        var id: Int =0
    }

    // 매개변수가 있고 클래스에 있는 프로퍼티를 초기화하기 위한 목적
    class Button(_id: Int){
        var id: Int = _id  //var id = _id //Int 생략 가능
    }

    // 클래스에 있는 프로퍼티를 매개변수로 정의할수 있음
    class Button(var _id: Int){
    }


    //예제
    class Button(var id: Int, val x: Int = 0, val y:Int = 0)

    fun main(args: Array<String>){
        val button1 = Button(100)
    }

    println("button1: ${button1.id} (${button.x} ${button.y})")
```

- 부생성자 (Secondary Constructor)
    부생성자는 클래스명 대신 Constructor라는 키워드를 사용해 정의한다.

```JavaScript
    
    class Button {
        var id: Int = 0
        contructor(id: Int){
            this.id = id
        }
    }

    // 부생성자에서 주생성자를 반드시 재호출 :this
    class Button(var id: Int) {
        var text: String = ""
        contructor(id:Int, text:String): this(id){
            this.text = text
        }
    }

    fun main(args: Array<String>){
        val Button1 = Button(100)
        val Button2 = Button(101, "button2")
    }


    //주생성자로 대체 가능
    class Button(var id:Int, var text:String="", var isCheckbox:Boolean=false)

```


## 클래스의 초기화 블록 (Initializer Block)
    초기화 블록은 주생성자 호출 직후 실행되며, 부생성자보다 먼저 실행된다.
```JavaScript
    class Button(var id:Int){
        var text:String=""
        init {
            println("Initializer Block:$id, $text")
        }
        constructor(id:Int, test:String): this(id) {
            this.text = text
            println("constructor(id, text) : ${this.text}")
        }
    }

```

```JavaScript
class Button{
    var id: Int =0
    var text:String=""
    init {
        println("Initializer Block 1:$id, $text")
    }
    constructor(id:Int){
        this.id = id
        println("constructor(id) : ${this.id}")
    }
    init {
        println("Initializer Block 2:$id, $text")
    }    
    constructor(id:Int, text:String): this(id) {
        this.text = text
        println("constructor(id, text) : ${this.id}, ${this.text}")
    }
    init {
        println("Initializer Block 3:$id, $text")
    }    
}

fun main(args: Array<String>) {
    println("Hello, world!")
    val Button = Button(100, "Button")
}

$ Hello, world!
$ Initializer Block 1:0, 
$ Initializer Block 2:0, 
$ Initializer Block 3:0, 
$ constructor(id) : 
$ constructor(id, text) : 



class Button(var id:Int){
    var text:String=""
    init {
        println("Initializer Block 1:$id, $text")
    }
    init {
        println("Initializer Block 2:$id, $text")
    }    
    constructor(id:Int, text:String): this(id) {
        this.text = text
        println("constructor(id, text) : ${this.id}, ${this.text}")
    }
    init {
        println("Initializer Block 3:$id, $text")
    }    
}

fun main(args: Array<String>) {
    println("Hello, world!")
    val Button = Button(100, "Button")
}

$ Hello, world!
$ Initializer Block 1:100, 
$ Initializer Block 2:100, 
$ Initializer Block 3:100, 
$ constructor(id, text) : 100, Button

```


## 클래스 상속
