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
- 초기화 블록은 주생성자 호출 직후 실행되며, 부생성자보다 먼저 실행된다.

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
```JavaScript
    final:      오버라이트 불가,                    클래스 멤버의 기본 변경자
    open:       오버라이트 가능,                    반드시 open을 명시해야 가능
    abstract:   반드시 오버라이트 해야 함,          추상 클래스의 멤버에만 붙일수 있다. 추상 멤버에는 구현이 있을 수 없다.
    override:   상위 멤버를 오버라이딩 하는 중,     오버라이드 하는 멤버는 기본적으로 open 상태. 항위 클래스에서 오버라이드를 금지상태면 final을 명시해야 함.

```

- 생성자와 오버라이드
```JavaScript
    open class Book(val title:String, var price:Int){
        open fun printInfo(){
            println("Title: $title, Price:$price")
        }
    }

    class EBook(title:String, price:Int, var url:String): Book(title, price){
        override fun printInfo(){
            println("Title:$title, Price:$price, URL:$url")
        }
    }

    fun main(args:Array<String>){
        val book = Book("bbb",200)
        val ebook = EBook("cccc", 1000, "aaaaa")
        book.printInfo()
        ebook.printInfo()
    }

$ Title: bbb, Price:200
$ Title:cccc, Price:1000, URL:aaaaa
```

- 오버라이드 금지 final
```JavaScript
    open class EBook(title:String, price:Int, var url:String): Book(title, price){
        final override printInfo(){
            println("Title:$title, Price:$price, URL:$url")
        }
    }

```

- 상속 클래스의 생성자를 사용 super
```JavaScript
    open class Book(val title:String, var price:Int) {
    }
    class EBook: Book {
        var url = ""
        constructor(title:String, price:Int, url:String): super(title, price){
        }
    }

```


## 인터페이스 선언
- interface
```JavaScript
    interface Clickable {
        fun click()
    }

    class Button:Clickable{
        override fun click() = println("click")
    }
```

```JavaScript
    interface Clickable {
        fun click()
        fun showOff() = println("show off")
    }

    class Button:Clickable{
        override fun click() = println("click")
    }

    fun main(args: Array<String>) {
        val button = Button()
        button.click()
        button.showOff()
    }

$ click
$ show off    
```


- 다중 인터페이스 상속
```JavaScript
    interface Clickable {
        fun click()
        fun showOff() = println("click off")
    }
    interface Focusable {
        fun setFocus(b:Boolean) = println("I ${if (b) "got" else "lost"} focus.")
        fun showOff() = println("focus off")
    }    

    class Button:Clieckable, Focusable{
        override fun click() = println("clicked.")
        override fun showOff() {
            super<Clickable>.showOff()
            super<Focusable>.showOff()
        }
    }

    fun main(args: Array<String>) {
        val button: Button()
        button.click()
        button.setFocus(true)
        button.showOff()
    }

$ clicked.
$ I got focus.
$ click off
$ focus off
```


- 인터페이스 클래스의 프로퍼티
```JavaScript
    interface User {
        val nickname: String
    }

    class PrivateUser(override val nickname:String): User
    class SubscribingUser(val email:String):User{
        override val nickname:String=getID()
        fun getID()=email.substringBefore('@')
    }

    fun main(args: Array<String>){
        println(PrivateUser("aaa").nickname)
        println(SubscribingUser("bbbb@cccc").nickname)
    }

$ aaa
$ bbbb
```


## 프로퍼티 (Property) getter, setter
- 멤버 변수의 필드와 게터, 세터를 묶어 프로퍼티라고 한다.
    값을 저장할수 없는 필드(Backing Field)
- 멤버 변수 선언시, 바로 뒤에 각 멤버에 대한 게터와 세터가 구현된다. 사용자가 직접 구현할때도 바로 뒤에 붙여서 구현해야 한다.
```JavaScript
    class Rectangle {
        var height:Int=0
        get()=field
        set(value){
            field=value
        }
        
        var width:Int=0
        get()=field
        set(value){
            field=value
        }
    }

    fun main(args:Array<String>){
        val rect = Rectangle()
        rect.height=10
        rect.width=20
        println("height:${rect.height}, width:${rect.width}")
    }

$ height:10, width:20
```

- 커스텀 접근자
```JavaScript
    class Rectangle(var height:Int, var width:Int) {
        val isSquare:Boolean
        get() = height==width
    }


    fun main(args:Array<String>){
        val rect = Rectangle(10,10)
        println("height:${rect.height}, width:${rect.width}, isSquare:${rect.isSquare}")
        rect.height=20
        println("height:${rect.height}, width:${rect.width}, isSquare:${rect.isSquare}")
    }

$ height:10, width:10, isSquare:true
$ height:20, width:10, isSquare:false
```


- 접근자의 가시성 변경자
    counter 프로퍼티는 var 타입이지만, set 앞에 private 접근자를 붙여 변경할수 없도록 함
    게터로 접근은 가능하지만, 세터로 값을 변경할 수 없음
```JavaScript
    class LengthCounter {
        var counter:Int=0
        private set

        fun addWord(word:String){
            counter+=word.length
        }
    }

    fun main(args: Array<String>){
        val lengthCounter = LengthCounter()
        //LengthCounter.counter = 1
        lengthCounter.addWord("aaa")
        println(lengthCounter.counter)
    }

$ 3
```

## 데이터 클래스
- 프로퍼티만 갖는 클래스 'data' 키워드 사용

```JavaScript
    data class Client(val name:String, val postalCode:Int)
```

- toString()
```JavaScript
    data Client(val name:String, val postalCode:Int) {
        override fun toString() = "Client(name= $name, postalCode= $postalCode)"
    }



    data class Client(val name:String, val postalCode:Int)

    fun main(args:Array<String>) {
        val client = Client("aaa", 1234)
        println(client)
    }

$ Client(name=aaa, postalCode=1234)

```

- equals()
```JavaScript
    class Client(val name:String, val postalCode:Int) {
        override fun equals(other: Any?) : Boolean {
            if (other == null || other !is Client) return false
            return name == other.name && postalCode == other.postalCode
        }
    }



    data class Client(val name:String, val postalCode:Int)

    fun main(args:Array<String>) {
        val client1 = Client("aaa", 1234)
        val client2 = Client("aaa", 1234)
        println(client1 == client2)
        println(client1.equals(client2))
    }

$ true
$ true

```

- hashCode()
```JavaScript
    class Client(val name:String, val postalCode:Int) {
        override fun equals(other: Any?) : Boolean {
            if (other == null || other !is Client) return false
            return name == other.name && postalCode == other.postalCode
        }

        override fun hashCode(): Int = name.hashCode() * 31 + postalCode
    }
    
    data class Client(val name:String, val postalCode:Int)

    fun main(args:Array<String>) {
        val clientset = hashSetOf(Client("aaa", 1234))
        println(clientset.contains(Client("aaa", 1234)))
    }


$ true
```

- copy()
```JavaScript
    data class Client(val name:String, val postalCode:Int)

    fun main(args:Array<String>) {
        val client1 = Client("aaa", 1234)
        val client2 = client1.copy(postalCode = 1236)
        println(client1)
        println(client2)
    }

$ Client(name=aaa, postalCode=1234)
$ Client(name=aaa, postalCode=1236)    
```