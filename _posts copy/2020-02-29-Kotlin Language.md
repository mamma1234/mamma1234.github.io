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


## 클래스의 확장
- 확장 함수(Extension Function) : 코틀린으로 변환할수 없는 자바코드를 처리해야 할 경우
- 확장 함수로 오버라이드할 수 없다.
- 확장 프로퍼티 : 반드시 커스텀 게터 get() 를 정의해 줘야 한다.
 
```JavaScript
    class Calculator {
        fun sum(a: Int, b: Int) = a+b
        fun minus(a: Int, b: Int) = a-b
    }

    fun Calculator.sum(a: Int, b: Int, c: Int) = sum(a,b)+c
    fun Calculator.minus(a: Int) = -a

    fun main(arga: Array<String>) {
        val calc = Calculator()
        println("1+2+3 = ${calc.sum(1,2,3)}")
        println("1 = ${calc.minus(1)}")
    }

$ 1+2+3 = 6
$ 1 = -1
```

## Null
- Non-Null 타입 : 컴파일시 에러 발생, NullPointerException 이 발생하지 않는다.
- Nullable 타입 : ? 문자를 사용하여 Null 값을 가질수 있도록 허용, Null Check 없이 바로 접근 불가능

```JavaScript
    class Bitmap(val width:Int, val height:Int) {
        val size: Int
        get() = width*height
        val map = ByteArray(size)
    }

    fun CreateBitmap(width:Int, height:Int):Bitmap? {
        if (width > 0 && height > 0) return Bitmap(width,height)
        else return null
    }

    fun main(args:Array<String>) {
        val bitmap : Bitmap? = CreateBitmap(10,10)
        if (bitmap != null) println(bitmap.size)
    }

$ 100
```

## Null Check
- Safe Calls : "?."
    왼쪽의 매개변수가 null이라면 null을 반환하며 구문을 종료하고, 아니라면 해당 변수를 Non-Null 타입으로 변환하여 프로퍼티에 접근한다.

```JavaScript

    fun main(args:Array<String>) {
        val bitmap : Bitmap? = CreateBitmap(10,10)
        if (bitmap != null) println(bitmap.size)
    }

    fun main(args:Array<String>) {
        val bitmap : Bitmap? = CreateBitmap(10,10)
        println(bitmap?.size)
    }    

    fun Person.cityName(): String {
        val city = this.company?.addr?.city
        return if (city != null) city else "Unkown"
    }
```

- Elvis(엘비스) 연산바:"?:"
    시계 방향으로 90도 회전하면 엘비스 프레슬리의 헤어스타일을 닮았다?
    왼쪽에 있는 값이 null이 결우 오른쪽에 있는 값을 대입한다.

```JavaScript
    fun Person.cityName(): String {
        val city = this.company?.addr?.city
        return city?:"Unkown"
    }

    fun Person.cityName(): String = this.company?.addr?.city?:"Unkown"
```

- !! Null 이 아님

```JavaScript

    fun main(args:Array<String>) {
        val bitmap : Bitmap? = CreateBitmap(10,10)
        bitmap : Bitmap? = CreateBitmap(10,10)
        println(bitmap!!.size)
    }

```

- let 함수
    let 함수를 사용해 Nullable 타입변수를 Non-Null 타입에 대입할 수 있다.

```JavaScript
    class Bitmap(val width:Int, val height:Int) {
        val size: Int
        get() = width*height
        val map = ByteArray(size)
    }

    fun CreateBitmap(width:Int, height:Int):Bitmap? {
        if (width > 0 && height > 0) return Bitmap(width,height)
        else return null
    }

    fun DrawBitmap(bitmap: Bitmap){
        println("DrawBitmap")
    }

    fun main(args:Array<String>) {
        val bitmap : Bitmap? = CreateBitmap(10,10)
        bitmap?.let {
            DrawBitmap(it)
        }
    }

```

    안전한 호출 연산자 ?.를 사용해서 'bitmap' 객체가 null인지 확인한후 null 이 아닐 경우에는 Non-Null 타입의 객체가 되어 let 함수를 실행한다. let 함수는 호출하는 객체를 인자로 넘기는 함수이므로 Non-Null 타입으로 변환된 bitmap 변수가 인자로 넘어와 DrawBitmap() 함수에 사용될 수 있다.
    it 연산자는 매개 변수가 하나 뿐일 경우 매개 변수 이름 대신 사용할 수 있는 키워드

## 제어 함수
- if

```JavaScript
    fun GetMax(a:Int, b:Int): Int = if (a<b) b else a

    fun GetMax(a:Int, b:Int): Int {
        return if (a<b) {
            println("b bigger than a")
            b
        } else {
            println("a bigger than b")
            a
        }
    }

```

- when

```JavaScript
    fun printValue(a:Int) {
        when(a) {
            1 -> println("value:1")
            2 -> println("value:2")
            else -> println("value is neigher 1 nor 2")
        }
    }
    
    fun printValue(a:Int, str:String) {
        when(a) {
            str.toInt() -> println("str is a")
            else -> prinln("str is not a")
        }
    }

    fun printValue(a:Int, str:String) {
        when(a) {
            in 1..10 -> println("str is (1~10)")
            in 10..20 -> println("str is (10~20)")            
            else -> prinln("str is not a")
        }
    }

    fun checkValue(a:Int) {
        when {
            a.isOdd() -> println("odd")
            a.isEven() -> println("even")
            else -> println("what")
        }
    }
```

- 스마트 캐스트 (Smart Cast)
    is 또는 !is 연산자를 통해 타입을 검사하여 객체 타입이 일치할 경우 객체가 해당 타입으로 자동 캐스팅 되는 기능

- while, do-while

- in
```JavaScript
    val oneToTen = 1..10

    fun isLetter(c: Char) = c in 'a'..'z'||c in 'A'..'Z'
    fun isNotDigit(c: Char) = c !in '0'..'9'

    fun recognize(c:Char) = when (c) {
        in '0' .. '9' -> "It's a digit"
        in 'a' .. 'z', in 'A' .. 'Z' -> "It's a letter"
        else -> "I don't klnow.. sorry TT"
    }

```

- for

```JavaScript
    for(i in 0..9) print("$i ")

    for(i in 10 downTo 1) print("$i ")

    for(i in 10 downTo 1 step 2) print("$i ")

    var array: Array<int> = arrayOf(1,2,3)
    for(i in 0 until array.size) print(array[1])
````

## 고차 함수와 람다
- 고차 함수 (High Order Function) : 매개변수 또는 반환 값으로 또 다른 함수가 사용되는 함수

```JavaScript
    button.setOnClickListener({ /* Click Event 함수 내용 */ })
```

- 람다(Lambdas) 식의 문법
{매개변수1: 타입, 매개변수2: 타입.. -> 반환형}

```JavaScript
    val sum = {x:Int, y:Int -> x+y }

    val sum:(Int, Int) -> Int = {x,y -> x+y}
```

- 익명함수 (Anonymous Function)

```JavaScript
    Calculator(2,1,{a:Int, b:Int -> a+b})

    fun Calculator(a:Int, b:Int, p:(Int, Int) -> Int){
        println("$a, $b -> ${p(a, b)}")
    }
```

## Collection

- List ; listOf : mutableListOf, arrayListOf
- Set ; set : mutableSetOf, hashSetOf, linkedSOf, sortedSetOf
- Map ; mapOf : mutableMapOf, hashMapOf, linkedMapOf, sortedMapOf

- 속성
val size:Int

- 함수
fun contains(element:E):Boolean
fun get(index:Int):E
fun indexOf(element:E):Int
fun isEmpty():Boolean
fun subList(formIndex:Int, toIndex:Int):List<E>

- 확장 기능
- MutableCollection 메서드



## 연산자 오버로딩 (operator)
- 이항연산자
a+b a.plus(b)
a-b a.minus(b)
a*b a.times(b)
a/b a.div(b)
a%b a.rem(b)

- 단항연산자
+a a.unaryPlus()
-a a.unaryMinus()
!a a.not()
++a, a++ a.inc()
--a, a-- a.dec()

- 복합 대입 연산자
a+=b a.plusAssign(b)
a-=b a.minusAssgin(b)
a*=b a.timesAssign(b)
a/=b a.divAssign(b)
a%=b a.remAssign(b)

- 비교 연산자
a==b a?.equals(b) ?: (b===null)
a!=b !(a?.equals(b) ?: (b===null))
a>b a.compareTo(b) > 0
a<b a.comapreTo(b) < 0
a>=b a.compareTo(b) >= 0
a<=b a.compareTo(b) <= 0

- 기타
in a.contain(b)
.. a.rangeTo(b)
a() a.invoke()


## 클래스 위임 (Class Delegation)
- by : 상속의 단점을 보완하기 위해 사용되는 데코레이터 패턴(Decorator Pattern) 의 구현을 줄이기 위해 제공

```JavaScript

    class CountingSet<T>: MutableCollection<T> {

    }


    class CountingSet<T>(val innerSet:MutableCollection<T>) : MutableCollection<T> by innerSet {

        override fun addAll(c:Collection<T>) : Boolean {
            .......
        }
    }


    fun main(args: Array<String>) {
        val lset = CountingSet<Int>(mutableListOf())
        val hset = CountingSet<Int>(hashSetOf())

        lset.addAll(listOf(1,2,3,2)) //override
        hset.addAll(listOf(1,2,3,2)) //source
    }
```

## 위임 프로퍼티 (Delegated Property)
- 위임 프로퍼티란, 프로퍼티의 접근자 게터(getter)와 세터(setter)를 다른 객체로 위임하는 방식
- 위임 받는 클래스에는 getValue() 메서드가 반드시 구현되어야 하며, 수정 가능한 var 타입의 경우 setValue() 메서드 역시 구현되어 있어야 한다.

- by

```JavaScript
    class Delegator(var value: Int){
        operator fun getValue(thisRef:Any?, property:KProperty<*>): Int {
            println("${property.name} get! $value")
            return value
        }
        operator fun setValue(thisRef:Any?, property:KProperty<*>, newValue: Int){
            println("${property.name} set! $newValue")
            value = newValue
        }
    }

    class Person(val name: String, age:Int, salary:Int) {
        var age:Int by Delegator(age)
        var salary:Int by Delegator(salary)
    }

    fun main(args:Array<String>?){
        val p = Person("test", 20, 2000)
        p.age = 21
        p.salary = 2100
        println("${p.name} - age:${p.age}, salary:${p.salary}")
    }
```

- by Lazy()
    지연 초기화를 위해 lazy() 메서드로 프로퍼티 접근을 위임할 수 있다.

```JavaScript
    data class Address(val name:String, var phone:String, var addr: String=""){

    }

    fun loadAddrBook(p:Person): List<Address> {
        return listOf(/* List */)
    }

    class Person(val name: String) {
        var addrBook by Lazy({loadAddrBook(this)})
    }

    fun main(args:Array<String>?){
        val p = Person("test")
        p.addrBook
    }
```

- Observable
    프로퍼티 변경시 필요한 기능을 Delegates, observable() 메서드에 람다 식과 함께 위임할 수 있다.

- Map
    Map, MutableMap 인터페이스에는 프로퍼티명 (property.name)을 이용한 getValue()와 setValue()가 구현되어 있어 위임 프로퍼티에 사용할 수 있다.


## 고차 함수와 람다의 활용
- 고차함수란 다른 함수를 인자로 받거나 함수를 반환하는 함수
- 람다 식의 정의에는 매개변수의 타입과 반환 타입이 명시되어야 하며, 매개 변수와 반환 타임은 Nullable이 될수 있다.
- 고차 함수 정의시 매개변수 또는 반환 타입의 함수 타입을 명확하게 정의해야 하며, 디폴트 값을 지정할 수 있다.
- 고차 함수와 람다를 이용해 소스 코드의 중복을 상당 부분 제거할 수 있다는 장점이 있다.


## 인라인 함수 (Inline Functions)
- 인라인 함수는 컴파일 단계에서 호출 방식이 아닌 코드 자체가 복사되는 방식으로 변환되며, 함수 앞에 inline 키워드를 붙여 사용한다.
- 람다 전달시 발생하는 메모리, 호출등의 오버 헤드를 감소시키기 위해 인라인 함수가 사용된다.
- 특정 람다를 인라인 방식에서 제외하고 싶을때는 noinline 키워드를 사용한다.

```JavaScript
    inline fun calculator(a: Int, b: Int, op: (Int, Int)->Int): Int {
        println("calculator body")
        return op(a,b)
    }

    fun main(args:Array<String>?){
        val result = calculator(1,2) {a:Int, b:Int -> a+b}
        println(result)
    }

- noinline : 인라인 함수 선언시 해당 파라미터 앞에 noinline 키워드를 붙여줌


$ calculator body
$ 3
```



## 람다에서의 리턴 (Return)
- Non-local Return
- 레이블을 이용한 Local Return
- 코틀린에서 return은 Non-Local return 과 Local return 이 있으며, Non-local return은 람다 안에 있는 return 구문이 바깥족 함수를 반환시키는 것을 의미한다.
- 람다 식에서는 return을 사용할 수 없지만, 인라인 함수에 사용되는 람다의 경우 Non-local return을 사용할 수 있다.
- 람다 식에서 Local return을 사용하고 싶다면 레이블을 이용해 사용할 수 있다.
- 일반적인 Local return을 사용할 수 있는 익명 함수를 람다 대신 사용할 수 있다.