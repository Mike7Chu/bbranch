---
layout: post
title:  "코틀린(Kotlin) 데이터클래스와 기타클래스 -10-"
date:   2020-08-23 22:20:22 +0900
image:  Kotlin-logo.png
tags:   [Kotlin]
---
## Overview  
데이터 클래스는 보통 데이터를 전달 혹은 다루기 위해서 사용합니다. 오늘은 데이터 클래스와 기타 클래스에 대해서 알아보겠습니다.  
<span style="color: grey">*이 글은 "Do it! 코틀린 프로그래밍"을 읽으면서 작성되었습니다.*</span>  
<br>
[1. 데이터 클래스](#데이터=클래스)  
[2. 기타 클래스](#기타=클래스)  
[3. 마치며](#마치며)  

------------------------  

## 데이터 클래스  
데이터 클래스는 표준이나 약속을 정하여 데이터를 주고 받을 때 쉽게 다루기 위해서 사용합니다. 데이터 클래스를 위해 data 키워드를 코틀린에서는 제공합니다.  
```kotlin
data class Customer(var name: String, var email: String)
```
<br>
데이터 클래스는 다음 조건을 만족해야 한다고 합니다.  
* 주 생성자는 최소한 하나의 매개변수를 가져야 한다.  
* 주 생성자의 모든 매개변수는 val, var로 지정된 프로퍼티여야 한다.  
* 데이터 클래스는 abstract, open, sealed, inner 키워드를 사용할 수 없다.  

즉, 데이터를 기술하는 용도로만 사용됩니다. 또한, 데이터 클래스가 생성하는 메서드는 다음과 같이 기술할 수 있습니다.  

|제공된 메서드|기능|  
|--------|--------|  
|equlas()|두 객체의 내용이 같은지 비교하는 연산자|  
|hashCode()|객체를 구별하기 위한 고유한 정숫값 생성, 데이터 세트나 해시 테이블을 사용하기 위한 하나의 생성된 인덱스|  
|copy()|빌더 없이 특정 프로퍼티만 변경해서 객체 복사하기|  
|toString()|데이터 객체를 읽기 편한 문자열로 반환하기|  
|compnoentN()|객체의 선언부 구조를 분해하기 위해 프로퍼티에 사용하는 메서드|  

--------------------------------------------

## 기타 클래스  
### 중첩 클래스  
코틀린에서 사용되는 기타 클래스들을 살표 보겠습니다. 우선 자바에서 정적 클래스를 크톨린에서 중첩 클래스로 다루고 있습니다. 정적 클래스의 경우 객체 생성 없이 가능한데요, 클래스 내부에 중첩으로 두어 사용합니다. 이는 다음과 같이 표현할 수 있습니다.  

```kotlin  
class Outer {
    val ov = 5
    class Nested {
        val nv = 10
        fun greeting( ) = "[Nested] Hello ! $nv" // 외부의 ov에는 접근 불가
    }
    fun outside() {
        val msg = Nested().greeting()
        println("[Outer]: $msg, ${Nested().nv}")
    }
}

fun main() {
    val output = Outer.Nested().greeting()
    println(output) // Staic처럼 객체 생성 없이 사용

    val outer = Outer()
    outer.outside() // 외부 클래스의 경우는 객체 생성 필요!!
}
```
>[Nested] Hello ! 10  
[Outer]: [Nested] Hello ! 10, 10  

<br>
Outer 클래스 안에 Nested라는 중첩 클래스가 선언되어 있습니다. 그리고 Outer.Nested().greeting()과 같은 방법으로 객체 생성 없이 호출될 수 있습니다. 하지만 외부 클래스의 메서드인 outside()의 경우 객체를 생성해줘야 호출 되는 것을 알 수 있습니다. 그리고 중첩 클래스에서 외부 프로퍼티인 ov를 접근할 수 없습니다.  

### 이너 클래스  
이너 클래스는 내부라는 뜻이지만, 키워드 inner로 표현하며 중첩 클래스와 달리 외부 멤버들을 접근할 수 있습니다.(*private 포함*)  
```kotlin  
class Smartphone(val model: String) {
    private val cpu = "Exynos"

    inner class ExternalStorage(val size: Int) {
        fun getInfo() = "${model}: Installed on $cpu with ${size}Gb"
    }
}

fun main() {
    val mySdcard = Smartphone("S7").ExternalStorage(32)
    println(mySdcard.getInfo())
}
```
>S7: Installed on Exynos with 32Gb  

<br>
private 멤버인 cpu를 접근 하는 것을 알 수 있습니다.  
### 지역 클래스  
지역 클래스는 특정 메서드의 블록이나 init 블록과 같이 블록 범위에서만 유효한 클래스 입니다. 즉 블록 범위를 벗어나면 더 이상 사용되지 않습니다.  
```kotlin
class Smartphone(val model: String) {
    private val cpu = "Exynos"

    inner class ExternalStorage(val size: Int) {
        fun getInfo() = "${model}: Installed on $cpu with ${size}Gb"
    }

    fun powerOn(): String {
        class Led(val color: String) {
            fun blink(): String = "Blinking $color in $model"
        }
        val powerStatus = Led("Red")
        return powerStatus.blink()
    }
}

fun main() {
    val mySdcard = Smartphone("S7").ExternalStorage(32)
    println(mySdcard.getInfo())

    val myphone = Smartphone("Note9")
    myphone.ExternalStorage(128)
    println(myphone.powerOn())
}
```
>S7: Installed on Exynos with 32Gb  
Blinking Red in Note9  

<br>
powerOn() 메서드의 경우 내부 Led 클래스가 있지만 이는 이 메서드 안에서만 접근 가능합니다.  
### 익명 객체  
일회성 객체를 생성하기 위해서 만드는 것을 말합니다. 다음과 같이 표현할 수 있습니다.  
```kotlin
interface Switcher {
    fun on(): String
}

val powerSwitch = object: Switcher {
    override fun on(): String {
        return powerStatus.blink()
    }
}
```
<br>
인터페이스 Switcher를 선언한 후 powerSwitch프로퍼티에 익명 객체를 선언해 주었습니다. 이 객체는 Switcher의 상속을 받아 on 메서드를 override 해주었습니다. 이렇게 되면 호출될 때마다 일회성으로 객체 인스턴스가 만들어 집니다.  

------------------------  

## 마치며
읽어주셔서 감사합니다.  
