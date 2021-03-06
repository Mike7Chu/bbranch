---
layout: post
title:  "코틀린(Kotlin) 변수 -2-"
date:   2020-06-28 08:00:22 +0900
image:  Kotlin-logo.png
tags:   [Kotlin]
---
## Overview  
안녕하세요. 코틀린의 변수에 대해서 알아보겠습니다. 코틀린은 기본적으로 프로젝트, 패키지, 모듈, 파일로 구성되어 있습니다. 이 안에서 변수는 어떻게 생성되고, 메모리에 담기는지 생각하면서 알아보도록 하겠습니다.  
<span style="color: grey">*이 글은 "Do it! 코틀린 프로그래밍"을 읽으면서 작성되었습니다.*</span>  
<br>
[1. 변수의 선언](#변수의-선언)  
[2. Null 확인](#null-확인)  
[3. 마치며](#마치며)  

------------------------  

## 변수의 선언  
변수는 기본적으로 값을 넣을 수 있는 공간과 같습니다. 변수를 선언하면 메모리 상에 공간이 할당되고, 이 공간에 값을 넣을 수 있습니다. 코틀린은 변수를 선언할 때 다음과 같이 선언할 수 있습니다.  
```kotlin
  val name1                     // 변수를 선언 자료형을 알지 못하므로 사용 불가
  val name2 = "Kildong"         // 변수를 선언 및 정의
  var name3: String = "Kildong" // 변수를 타입까지 정의
```
<br>
코틀린에서는 **선언 키워드 변수이름 : 자료형 = 값**으로 변수를 선언 및 정의하고 있습니다.
위의 예시에서 첫번째 줄에서 변수는 에러가 날 것입니다. 코틀린은 자료형을 반드시 지정해야합니다.
또한 val과 var이 있습니다. var같은 경우 변수를 뜻하며 초기화 후 값을 변경할 수 있습니다. val의 경우 값이 할당 된 후 더 이상 변경할 수 없습니다.  
그리고 두번째 줄과 같이 자료형 없이 선언하면 코틀린에서는 알맞는 자료형을 자동할당 합니다. 이를 오토타입이라고도 합니다.  

------------------------  

## Null 확인  
Kotlin은 변수에 반드시 자료가 할당되어 있어야 합니다. 만약 null이라면 컴파일 시 에러를 발생 시킵니다. 에러를 발생시키지 않기 위해서 코틀린에서 Null을 어떻게 처리하는지 알아보겠습니다.  
<br>
만약 Null이 할당된 변수에 접근하면 NullPointerException이 발생하게 됩니다. 코틀린은 Null에 대한 안전한 처리를 위해서 변수에 값이 할당되도록 되어 있습니다. 하지만 null을 할당해야할 경우 코틀린에서는 다음과 같이 변수를 선언 합니다.  
```kotlin
  var str1 : String? = "Hello Kotlin"
  str1 = null
  println("str1: $str1 length: $(str1?.length)") // 세이프 콜로 호출
```
<br>
? 심볼을 자료형 뒤에 추가하면 됩니다. ? 심볼을 추가함으로써 명시적으로 null을 가질 수 있는 변수라고 하는 것입니다. 또한 세이프 콜이라고 하여 null 객체 뒤에 ? 심볼을 추가하면 null이 아니면 호출하도록 하고 있습니다. 이를 엘비스 연산자(*?*)와 함께 사용하면 다음과 같이 표현할 수 있습니다.  
```kotlin
  var str1 : String? = "Hello Kotlin"
  str1 = null
  println("str1: $str1 length: $(str1?.length ?:-1)") // 세이프 콜로 호출
```
<br>
엘비스 연산자는 널인지 확인하여 널인 경우 오른쪽 값을 널이 아닌 경우 왼쪽 값을 반환해줍니다. 이를 통해서 null에 대해서 안전하게 처리할 수 있습니다. 이게 많은 사람들이 말하는 코틀린의 장점 입니다.  

------------------------  

## 마치며
오늘은 코틀린의 변수에 대해서 살펴봤습니다. 사실 연산자까지 공부했었는데 연산자의 경우 JAVA와 크게 다르지 않아 다루지 않았습니다. 코틀린은 null 회피 말고도 JAVA에서 사용했던 표현을 많이 간결하게 사용할 수 있습니다. 아직 경험치가 부족하여 이런 부분은 다루기 힘들고 더욱 공부하여 포스팅 하도록 하겠습니다.  