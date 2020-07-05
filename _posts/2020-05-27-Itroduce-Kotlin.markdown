---
layout: post
title:  "코틀린(Kotlin) 개요 -1-"
date:   2020-05-27 23:47:26 +0900
image:  Kotlin-logo.png
tags:   [Kotlin, sublime]
---
## Overview  
안녕하세요. 코틀린 공부를 시작하게 되면서, 코틀린을 끄적이려고 합니다. 오늘부터 차근차근 변수부터 안드로이드 구현까지 적도록 하겠습니다.  
[1. Kotlin이란](#kotlin이란)  
[2. Kotlin의 이점](#kotlin의-이점)  
[3. Kotlin 설치](#kotlin-설치)  

------------------------  

## Kotlin이란  
*코틀린(Kotlin)은 JVM에서 동작하는 프로그래밍 언어이다. 2011년 7월, 젯브레인사가 공개하였다.* [*출처 wiki*](https://ko.wikipedia.org/wiki/%EC%BD%94%ED%8B%80%EB%A6%B0_(%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D_%EC%96%B8%EC%96%B4))  
<br>
코틀린은 jetbrains에서 개발한 JVM에서 동작하는 언어입니다. jetbrains 사는 다양한 언어를 지원하는 IntelliJ와 크로스플랫폼까지 지원하는 CLion을 구현한 거대한 개발사 입니다. 이러한 회사에서 개발한 언어는 지원도 당연히 보장될테고, 현재 안드로이드에서도 공식언어로 채택했을테니 안넘어갈 이유가 없겠죠? 한번 코틀린을 쓰면 무엇이 좋은지 살펴보도록 하겠습니다.  

------------------------  

## Kotlin의 이점  
Kotlin을 쓸 경우 공식홈페이지에서는 다음을 특징으로 말하고 있습니다.  
<br>
Concise : 간결함 입니다. java를 쓸 때보다 간결한 표현이 가능합니다. 홈페이지의 예시를 보면 data class에서는 기본적인 메소드를 제공하기 때문에, 특정 type의 data가 필요할 때 한줄로 할 수 있습니다. 또한 람다식을 이용하여 리스트의 멤버를 필터링 할수 있고, 싱글톤 패턴을 object 타입으로 쉽게 만들 수 있습니다.
<br>
```kotlin
/*
 Create a POJO with getters, setters, 'equals()', 'hashCode()', 'toString()' and 'copy()' in a single line:
*/

data class Customer(val name: String, val email: String, val company: String)

// Or filter a list using a lambda expression:

val positiveNumbers = list.filter { it > 0 }

// Want a singleton? Create an object:

object ThisIsASingleton {
    val companyName: String = "JetBrains"
}
```
<br>
Safe : Null Pointer 같은 에러를 피할 수 있다고 합니다. compile 단계에서 null pointer 에러를 찾으면서 더 안정적인 프로그램을 만들 수 있습니다. 그리고 타입 체크를 통해서 객체 type에 대해서 또한 안정적으로 구현할 수 있습니다.
```kotlin
/*
 Get rid of those pesky NullPointerExceptions, you know, The Billion Dollar Mistake
*/

var output: String
output = null   // Compilation error

// Kotlin protects you from mistakenly operating on nullable types

val name: String? = null    // Nullable type
println(name.length())      // Compilation error

// And if you check a type is right, the compiler will auto-cast it for you

fun calculateTotal(obj: Any) {
    if (obj is Invoice)
        obj.calculateTotal()
}
```
<br>
Interoperable : 호환입니다. Kotlin은 기존 라이브러리를 사용할 수 있다고 합니다. java 라이브러리는 바로 가져와서 쓸 수 있다고하니, 기존 jvm이나 Android 프로젝트 마이그레이션이 편리 합니다.  

------------------------  

## Kotlin 설치  
저는 sublime을 주로 사용하는데요. sublime은 package control를 통해서 쉽게 설치 가능합니다. ctrl+shift+p 를 누른 뒤 package control : Install Package 를 하신 후 Kotlin만 검색하면 됩니다.  

------------------------


## 마치며
오늘은 Kotlin을 설치까지 알아보았습니다. 다음 시간에는 코틀린 변수와 함수에 대해서 알아보도록 하겠습니다.  