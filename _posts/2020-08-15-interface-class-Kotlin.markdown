---
layout: post
title:  "코틀린(Kotlin) 인터페이스 -9-"
date:   2020-08-15 05:20:22 +0900
image:  Kotlin-logo.png
tags:   [Kotlin]
---
## Overview  
지난시간 추상클래스에 이어서 인터페이스를 다루겠습니다.  
<span style="color: grey">*이 글은 "Do it! 코틀린 프로그래밍"을 읽으면서 작성되었습니다.*</span>  
<br>
[1. 인터페이스](#인터페이스)  
[2. 마치며](#마치며)  

------------------------  

## 인터페이스  
인터페이스는 추상클래스와 비슷하지만 인터페이스는 클래스가 아닙니다. 따라서 클래스가 여러 인터페이스를 상속받을 수 있습니다. 이러한 점 때문에 인터페이스를 가져다 씁니다. 코틀린에서는 인터페이스에서 추상메소드 뿐만 아니라 일반메소드도 정의할 수 있습니다.  
```kotlin  
interface Pet {
    var category:String
    fun feeding()
    fun petting() {
        println("Keep petting!")
    }
}

class Cat(override var category: String): Pet {
    override fun feeding() {
        println("Feed the cat a tuna can")
    }

}

fun main() {
    val obj = Cat("small")
    println("Pet categiry : ${obj.category}")
    obj.feeding()
    obj.petting()
}
```
>Pet categiry : small  
Feed the cat a tuna can  
Keep petting!  

<br>
인터페이스는 일반메소드를 정의해주면 stub시 따로 추가로 정의하지 않아도 됩니다. JAVA8부터는 default prefix로 구분을 하는데 코틀린은 명시할 필요없이 자동으로 됩니다. 더 편리하고 간단하다고 말씀 드릴 수 있습니다. Cat을 보면 콜론을 통해서 Pet을 가져왔는데 상속을 받았다고 보면 됩니다.  

인터페이스 위임은 다음과 같이 표현됩니다.  
```kotlin
interface Nameable {
    var name: String
}

class StaffName : Nameable {
    override var name: String = "Sean"
}

class Work : Runnable {
    override fun run() {
        println("work.....")
    }
}

class Person(name: Nameable, work: Runnable): Nameable by name, Runnable by work

fun main() {
    val person = Person(StaffName(),Work())
    println(person.name)
    person.run()
}
```  
>Sean  
work.....  

<br>
위임을 통해 상속을 받으면 코드를 더 간결하게 표현할 수 있습니다. 만약 위임이 없었다면, 다음과 같이 접근해야 합니다.  
person.Nameable.name, person.Runnable.run()  
또한 위임을 통해 여러 인터페이스를 상속받은 클래스로부터 특정 인터페이스 영역만 상속받을 수 있습니다.  

------------------------  

## 마치며
인터페이스까지 마쳤는데, 나머지 클래스들은 다음 포스팅에서 다루고 그다음부터는 코틀린 표준 라이브러리를 다룰 예정입니다.  
읽어주셔서 감사합니다.  
