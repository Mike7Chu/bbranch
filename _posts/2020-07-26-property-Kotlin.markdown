---
layout: post
title:  "코틀린(Kotlin) 프로퍼티(1) -6-"
date:   2020-07-26 23:30:22 +0900
image:  Kotlin-logo.png
tags:   [Kotlin]
---
## Overview  
코틀린에는 프로퍼티가 있습니다. 지난 시간에 잠깐 소개했었는데요, 오늘은 프로퍼티에 대해서 알아보겠습니다.    
<span style="color: grey">*이 글은 "Do it! 코틀린 프로그래밍"을 읽으면서 작성되었습니다.*</span>  
<br>
[1. 프로퍼티란](#프로퍼티란)  
[2. lateinit 및 lazy](#lateinit 및 lazy)  
[3. 마치며](#마치며)  

------------------------  

## 프로퍼티란  
프로퍼티는 코틀린에서 변수와 메소드가 같이 포함된 클래스의 필드 입니다. 자바와 다르게 변수를 선언 하면 변수에 대한 세터와 게터인 set, get 메소드가 같이 생성 됩니다. 따라서 자바와 다르게 get() set() 메소드를 구현할 필요 없이 아래와 같이 간단하게 구현하여 사용할 수 있습니다.  
```kotlin
  class User(_id:Int, _name:String, _age:_Int) {
    //프로퍼티
    val id:Int = _id
    var name:String = _name
    var age:Int = _age
  }
  fun main() {
    val user = User(1, "Sean", 30)

    val name = user.name   //name = user.getName()
    user.age = 41           // user.age = user.setName(41)

    println("name: $name, ${user.age}")
  }
```
>name: Sean, 41

<br>
게터와 세터는 위 주석처럼 getName과 setName을 그대로 쓴 것과 같이 '.' 으로 바로 접근할 수 있습니다. 여기서 만약 게터와 세터를 임의로 변경을 하고 싶다면 어떻게 해야할까요? 프로퍼티 선언 시 바로 정의를 해주면 됩니다.  
```kotlin
  class Bird (var name: String, var wing: Int, var beak: String, var color: String) {

    fun fly() = println("Fly wing: $wing")
    fun sing(vol: Int) = println("Sing vol: $vol")
  }
```
<br>
클래스 명시시 생성자를 함께 할 수 있습니다. 클래스 옆에 있는 생성자를 주 생성자, constructor 메소드를 부 생성자라고 합니다. 만약 생성자에서 처리해야할 구문이 존재한다면, 초기화(**init**) 블록을 넣을 수 있습니다.  
```kotlin
  class User(_id:Int, _name:String, _age:Int) {
    //프로퍼티
    val id:Int = _id
    var name:String = _name
        set(value) {
            println("The name was changed")
            field = value.toUpperCase()
        }
    var age:Int = _age
  }
  fun main() {
    val user = User(1, "kildong", 35)

    user.name = "coco"
    println("name: ${user.name}, ${user.age}")
  }
```
>The name was changed
name: COCO, 35

<br>
name 에 coco를 재 정의 시 세터가 호출되어 모두 소문자에서 대문자로 바뀌었습니다. 이렇게 확장 해줄 수도 있습니다. 그런데 여기서 **field와 value**는 무엇일까요? field와 value는 보조 필드라고 해서 세터와 게터에서 사용 됩니다. 실제로 name = value는 name = this.setName(value)와 같습니다. 만약 게터를 get() = field로 재정의 한다면 get() = get() 과 같아서 StackOverflowError가 발생할 수 있습니다.  

------------------------  

## lateinit 및 lazy  
 lateinit은 이름 그대로 정의를 늦게 하는 것입니다. 다른 자원이 정의 된 뒤 처리를 해야하거나, 정의되어야 할 시점이 뒤늦게 있을 경우 lateinit 심볼을 이용해서 정의를 뒤로 미룰 수 있습니다.  
```kotlin
  class Person {
    lateinit var name: String
    fun test() {
    if(!::name.isInitialized) {
      println("not initialized")
    } else {
      println("initialized")
      }
    }
  }

  fun main() {
    val kildong = Person()
    kildong.test()
    kildong.name = "Kildong"
    kildong.test()
    println("name = ${kildong.name}")
  }
```
>not initialized
initialized
name = Kildong

<br>
처음 test()호출 시 not initialized를 출력하고 두 번째 호출 시 initialized를 호출합니다. 여기서 isInitialized는 코틀린의 표준 함수 API이며 프로퍼티 참조를 위해 콜른::를 사용한 것입니다. lateinit은 다음과 같은 특징이 있습니다.  
* var로 선언된 프로퍼티만 가능하다.  
* 프로퍼티에 대한 게터와 세터를 사용할 수 없다.  

lateinit은 var로 선언된 프로퍼티만 가능합니다. 또한, 클래스에도 클래스 타입의 var프로퍼티가 존재할 경우 적용할 수 있습니다.
만약 val로 선언된 프로퍼티에 사용하려면 어떻게 해야할까요? lazy를 사용하면 됩니다.  
```kotlin
class lazyTest {
    init {
        println("init block")
    }

    val subject by lazy {
        println("lazy initialized")
        "Kotlin Programing"
    }
    fun flow(){
        println("not initialized")
        println("subject one: $subject")
        println("subject two: $subject")
    }
}

fun main() {
    val test = lazyTest()
    test.flow()
}
```
>init block
not initialized
lazy initialized
subject one: Kotlin Programing
subject two: Kotlin Programing

<br>
출력 결과를 보면, subject 바로 초기화 되지않고, subject one 호출 시 초기화 되었습니다. 여기서 by lazy를 사용하였는데요, by lazy는 람다식 형태 입니다. by에 의해서 subject는 lazy를 위임 받았습니다. 여기서 핵심은 접근하는 시점에 프로퍼티가 초기화 되었다는 것입니다. lazy의 특성을 정리하면 다음과 같습니다.
* 호출 시점에 by lazy{...} 정의에 의해 블록 부분의 초기화를 진행한다.  
* 불변의 변수 선언인 val에서만 사용 가능하다.(읽기전용)  
*  val이므로 값을 다시 변경할 수 없다.  

------------------------  

## 마치며
오늘은 프로퍼티에 대해서 알아보았습니다. 프로퍼티에 들어오면서 점점 처음 보는 것들이 늘어납니다. 오늘 by를 잠시 언급했었는데요, 다음주에는 by에 대해서 더 알아보겠습니다.