---
layout: post
title:  "코틀린(Kotlin) 프로퍼티(2) -7-"
date:   2020-08-02 12:30:22 +0900
image:  Kotlin-logo.png
tags:   [Kotlin]
---
## Overview  
프로퍼티와 관련하여 by(위임자)와, companion 객체를 정리하겠습니다.  
<span style="color: grey">*이 글은 "Do it! 코틀린 프로그래밍"을 읽으면서 작성되었습니다.*</span>  
<br>
[1. by 위임자](#by-위임자)  
[2. Companion 객체](#Companion-객체)  
[3. 마치며](#마치며)  

------------------------  

## by 위임자  
코틀린에서 클래스나 프로퍼티를 위임할 수 있습니다. 위임을 하여 위임 받는 클래스가 위임하는 클래스의 멤버를 참조 없이 호출할 수 있습니다. 여기서 프로퍼티 위임은 게터나 세터를 다른클래스에게 위임하는 것을 의미합니다. 표현은 다음과 같이 할 수 있습니다.  
> **\<val\|var\|class\> 프로퍼티 혹은 클래스 이름: 자료형 by 위임자**  

```kotlin
interface Car {
    fun go(): String
}

class VanImpl(val power: String): Car {
    override fun go() = "은 적제하며 $power 을 가집니다."
}

class SportImpl(val power: String): Car {
    override fun go() = "은 경주용에 사용되며 $power 을 가집니다."
}

class CarModel(val model: String, impl: Car): Car by impl {
    fun carInfo() {
        println("$model ${go()}")
    }
}

fun main() {
    val myDamas = CarModel("Damas 2010", VanImpl("100마력"))
    val my350z = CarModel("350Z 2008", SportImpl("350마력"))

    myDamas.carInfo()
    my350z.carInfo()
}
```
>Damas 2010 은 적제하며 100마력 을 가집니다.  
350Z 2008 은 경주용에 사용되며 350마력 을 가집니다.  

<br>
지난번에 lazy 를 배웠었는데요, lazy도 잘보면 위임자를 통해서 사용하고 있습니다. *val subject by lazy* 그 외에도 코틀린에서 프로퍼티를 위임하는 객체인 Delegates로부터 사용할 수 있는 위임자인 observable(), vetoable() 메소드 등이 있습니다. 이 메소드들은 값이 변경되기 전 또는 후처리를 정의할 수 있습니다.  
```kotlin
import  kotlin.properties.Delegates

class User {
    var name: String by Delegates.observable("NONAME") {
        prop, old, new ->println("$old -> $new")
    }
}

fun main() {
    val user = User()
    user.name = "Kildong"
    user.name = "Dooly"

    var max: Int by Delegates.vetoable(0) {
        prop, old, new -> new > old
    }

    println("max = $max")
    max = 10
    println("max = $max")

    max = 5
    println("max = $max")
}
```
>NONAME -> Kildong  
Kildong -> Dooly  
max = 0  
max = 10  
max = 10    

------------------------  

## Companion 객체  
코틀린에서는 정적 변수를 사용할 때 static 키워드가 없는 대신 컴패니언 객체를 사용합니다. 정적 변수의 경우는 객체를 생성 없이도 접근할 수 있는 특징이 있습니다. 
```kotlin
class Person {
    var id: Int = 0
    var name: String = "Youngdeok"

    companion object {
        var language: String = "Korean"
        fun work() {
            println("working...")
        }
    }
}

fun main() {
    println(Person.language)
    Person.language = "English"
    println(Person.language)
    Person.work()
}
```
>Korean  
English  
working...  

<br>
객체 생성 없이 사용되는 companion object를 확인하였습니다. 만약 자바와 연동해서 사용하려면 정적 변수나 메소드를 접근해야하는데, 이 경우는 애노테이션 @JvmStatic을 붙여서 사용한다고 하면 됩니다.*(코틀린에서 자바로 접근하는 경우만 사용 반대의 경우는 그냥 접근 가능합니다.)* 여기서는 귀찮기도 하고... 다루지 않겠습니다.  
object 키워드의 경우 클래스를 새로 생성하지 않고, 객체를 생성하고 싶을 때 사용하는 키워드 입니다. 자바의 익명 내부 클래스 처럼 새로운 클래스 선언을 하지 않고, 변형된 객체를 생성하기 위함 입니다. 자바에서 이 객체를 접근하려면 INSTANCE 키워드를 사용하여 접근 합니다.  
```kotlin
object OCustomer {
    var name = "Kildong"
    fun greeting() = println("Hello World!")
    val HOBBY = Hobby("basketball")
    init {
        println("Init!")
    }
}

class CCustomer {
    companion object {
        const val HELLO = "hello"
        var name = "Joosol"
        @JvmField val HOBBY = Hobby("Football")
        @JvmStatic fun greeting() = println("Hello World!")
    }
}

class Hobby(val name: String)

fun main() {
    OCustomer.greeting()
    OCustomer.name = "Dooly"
    println("name = ${OCustomer.name}")
    println(OCustomer.HOBBY.name)

    CCustomer.greeting()
    println("name = ${CCustomer.name}, HELLO = ${CCustomer.HELLO}")
    println(CCustomer.HOBBY.name)
}
```
>Init!  
Hello World!  
name = Dooly  
basketball  
Hello World!  
name = Joosol, HELLO = hello  
Football  

@JvmFeild의 경우는 java에서 프로퍼티를 사용하고 싶을 경우 사용하는 애노테이션 입니다. object의 경우 호출 시 생성 되는 것을 확인할 수 있습니다.  

------------------------  

## 마치며
읽어주셔서 감사합니다.  