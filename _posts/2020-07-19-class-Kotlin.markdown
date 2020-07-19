---
layout: post
title:  "코틀린(Kotlin) 클래스 -5-"
date:   2020-07-19 14:30:22 +0900
image:  Kotlin-logo.png
tags:   [Kotlin]
---
## Overview  
객체 지행 프로그래밍에서는 클래스라는 개념이 빠질 수 없습니다. 많은 객체를 클래스로 구현하기 때문입니다. 만약 클래스가 익숙하지 않으시다면 제 블로그가 도움이 되지 않을 수 있습니다. 코틀린에서 클래스를 어떻게 표현하는지 알아보겠습니다.  
<span style="color: grey">*이 글은 "Do it! 코틀린 프로그래밍"을 읽으면서 작성되었습니다.*</span>  
<br>
[1. 클래스의 생성자](#클래스의-생성자)  
[2. 클래스 상속](#클래스-상속)  
[3. 마치며](#마치며)  

------------------------  

## 클래스의 생성자  
코틀린에서의 클래스는 메소드(함수)와 프로퍼티(변수)를 가집니다. 변수 또는 필드라고 하지않고 프로퍼티라고 지칭하는 이유는 프로퍼티마다 내부적으로 자체의 접근 메소드를 가지고 있기 때문이라고 합니다.  
클래스를 만들어 볼텐데요. 일반적으로 클래스를 호출하면 다음과 같이 정의하고 호출할 수 있습니다.  
```kotlin
  class Bird{
    var name: String
    var wing: Int
    var beak: String
    var color: String

    constructor(name: String, wing: Int, beak:String, color: String){
      this.name = name
      this.wing = wing
      this.beak = beak
      this.color = color
    }

    fun fly() = println("Fly wing: $wing")
    fun sing(vol: Int) = println("Sing vol: $vol")
  }

  fun main(){
    val coco = Bird("mybird",2, "short", "blue")

    coco.color="yellow"
    println("cooc.color: ${coco.color}")
    coco.fly()
    coco.sing(3)
  }
```
>cooc.color: yellow  
Fly wing: 2  
Sing vol: 3  

<br>
main문을 확인하면 Bird 클래스를 매개변수와 함께 coco로 생성하고 coco의 color를 변경하는 예제입니다. 여기서 **constructor**메소드를 볼 수 있는데요, 이것이 생성자 입니다. 일반적으로 java에서 위와 같이 표현을 하고 있고, 다만 다른 것은 new 키워드가 사라졌습니다. Kotlin에서는 new 없이도 객체를 생성할 수 있습니다.  
 생성자를 다르게도 표현할 수 있는데요. 다음 예제를 보시면 됩니다.  
```kotlin
  class Bird (var name: String, var wing: Int, var beak: String, var color: String) {

    fun fly() = println("Fly wing: $wing")
    fun sing(vol: Int) = println("Sing vol: $vol")
  }
```
<br>
클래스 명시시 생성자를 함께 할 수 있습니다. 클래스 옆에 있는 생성자를 주 생성자, constructor 메소드를 부 생성자라고 합니다. 만약 생성자에서 처리해야할 구문이 존재한다면, 초기화(**init**) 블록을 넣을 수 있습니다.  
```kotlin
  class Bird (var name: String, var wing: Int, var beak: String, var color: String) {

    init {
      println("----------초기화 블록 시작----------")
      println("이름은 $name, 부리는 $beak")
      this.sing(3)
      println("----------초기화 블록 끝----------")
    }

    fun fly() = println("Fly wing: $wing")
    fun sing(vol: Int) = println("Sing vol: $vol")
  }

  fun main(){
    val coco = Bird("mybird",2, "short", "blue")

    coco.color="yellow"
    println("cooc.color: ${coco.color}")
    coco.fly()
    coco.sing(3)
  }
```
>----------초기화 블록 시작----------  
이름은 mybird, 부리는 short  
Sing vol: 3  
----------초기화 블록 끝----------  
cooc.color: yellow  
Fly wing: 2  
Sing vol: 3  

<br>
클래스 생성 시 init 블록이 처리되는 것을 확인할 수 있습니다. 클래스 옆에 생성자가 있고, 명확히 구분 되므로 더 가독성있는 코드를 만들 수 있습니다.  

------------------------  

## 클래스 상속  
 코틀린의 모든 클래스는 묵시적으로 Any 클래스로부터 상속을 받습니다. 상속에 있어서는 **open** 키워드를 알아야 합니다. 클래스 앞에 open 키워드를 붙이면 상속할 수 있는 클래스로 선언하고 open 키워드가 없으면 상속할 수 없는 클래스 입니다. 다음을 보면 쉽게 이해할 수 있습니다.  
```kotlin
  open class Bird (var name: String, var wing: Int, var beak: String, var color: String) {

    fun fly() = println("Fly wing: $wing")
    fun sing(vol: Int) = println("Sing vol: $vol")
  }

  class Lark(name: String, wing: Int, beak: String, color: String) : Bird(name, wing, beak, color) {
    fun singHiton() = println("Happly Song!")
  }

  class Parrot : Bird {
    val language: String

    constructor(name: String, wing: Int, beak: String, color: String, language: String) : super(name, wing, beak, color) {
        this.language = language
    }

    fun speak() = println("Speak: $language")
 }
  fun main(){
    val coco = Bird("mybird",2, "short", "blue")
    val lark = Lark("mylark", 2, "long", "brown")
    val parrot = Parrot("myparrot", 2, "short", "multiple", "korean")

    println("Coco: ${coco.name}, ${coco.wing}, ${coco.beak}, ${coco.color}")
    println("Lark: ${lark.name}, ${lark.wing}, ${lark.beak}, ${lark.color}")
    println("Parrot: ${parrot.name}, ${parrot.wing}, ${parrot.beak}, ${parrot.color}, ${parrot.language}")
    lark.singHiton()
    parrot.speak()
    lark.fly()
  }
```
>Coco: mybird, 2, short, blue  
Lark: mylark, 2, long, brown  
Parrot: myparrot, 2, short, multiple, korean  
Happly Song!  
Speak: korean  
Fly wing: 2  

open 키워드를 통해 Bird클래스를 상속 가능하게 해주고 변수 인자를 주듯이 Bird를 주어 상속받도록 하였습니다. 상속을 받았기 때문에 lark.fly() 시 Bird의 fly()가 호출되는 것을 확인하였습니다. 그리고 open 키워드는 클래스 말고도 다형성을 위해 오버라이딩 할 때도 사용할 수 있습니다.  
```kotlin
  open class Bird (var name: String, var wing: Int, var beak: String, var color: String) {

    fun fly() = println("Fly wing: $wing")
    open fun sing(vol: Int) = println("Sing vol: $vol")
  }

  class Parrot (name: String, wing: Int, beak: String, color: String, var language: String) : Bird(name, wing, beak, color) {

    fun speak() = println("Speak: $language")
    override fun sing(vol: Int) {
        println("I'm a parrot! The volume level is $vol")
    }
  }
  fun main(){
    val coco = Bird("mybird",2, "short", "blue")
    val parrot = Parrot("myparrot", 2, "short", "multiple", "korean")

    println("Parrot: ${parrot.name}, ${parrot.wing}, ${parrot.beak}, ${parrot.color}, ${parrot.language}")
    parrot.sing(5)
    parrot.speak()
  }
```
>Parrot: myparrot, 2, short, multiple, korean  
I'm a parrot! The volume level is 5  
Speak: korean  

------------------------  

## 마치며
이제 객체 들어왔습니다. 다음 단원은 프로퍼티던데요. 열심히 공부해서 준비하겠습니다. 읽어주셔서 감사합니다.  