---
layout: post
title:  "코틀린(Kotlin) 조건문 반복문 -4-"
date:   2020-07-12 09:20:22 +0900
image:  Kotlin-logo.png
tags:   [Kotlin]
---
## Overview  
조건문과 반복문은 프로그램 흐름제어에서 많이 쓰입니다. 코틀린에서는 어떻게 표현하고, 더 간결하게 사용할 수 있는지 알아보겠습니다.  
<span style="color: grey">*이 글은 "Do it! 코틀린 프로그래밍"을 읽으면서 작성되었습니다.*</span>  
<br>
[1. 조건문](#조건문)  
[2. 반복문](#반복문)  
[3. 마치며](#마치며)  

------------------------  

## 조건문  
조건문은 어떠한 조건에 따라 프로그램을 다르게 실행시키고 싶을 때 사용합니다. 코틀린은 java와 크게 다르지 않지만, 더 간결하게 사용할 수 있는 방법이 있습니다. 우선 일반적으로 사용하는 조건문을 알아보겠습니다.  
```kotlin
  fun main(){
    print("Enter the score: ")
    val score = readLine()!!.toDouble()
    var grade: Char = 'F'

    if(score >= 90.0) {
        grade = 'A'
    } else if(score >= 80.0 && score <= 89.9) {
        grade = 'B'
    } else if(score >= 70.0 && score <= 79.9) {
        grade = 'C'
    } else {
      grade = 'D'
    }

    println("Score: $score Grade: $grade")
  }
```
<br>
readLine()으로부터 입력을 받아 score에 따른 grade를 결정하는 조건문 입니다. 여기서 !!은 not-null의 뜻으로 null값이 절대 오지 않는다는 표현입니다. 만약 null 값이 오게되면 에러를 발생합니다. 이제 여기서 코틀린 만의 간결한 표현을 한다면 람다식을 이용했던 방식으로 바로 grade 변수에 정의를 내릴 수 있습니다.  
```kotlin
  fun main(){
    print("Enter the score: ")
    val score = readLine()!!.toDouble()

    var grade: Char = if(score >= 90.0)
        'A'
    else if(score >= 80.0 && score <= 89.9)
        'B'
    else if(score >= 70.0 && score <= 79.9)
        'C'
    else
        'D'

    println("Score: $score Grade: $grade")
  }
```
<br>
그리고 논리 연산자로 &&를 사용하여 두개의 조건식으로 범위를 나타내었습니다. 코틀린에서는 범위 연산자가 in이 존재하여 다음과 같이 간결하게 표현 가능합니다.  

>**변수 이름 in 시작값..마지막값**  

범위 연산자는 시작값부터 마지막값까지 포함하는 범위를 계산합니다. 그에 따라 시작값과 마지막값도 포함 됩니다. 표현하면 아래와 같습니다.  
```kotlin
  fun main(){
    print("Enter the score: ")
    val score = readLine()!!.toDouble()

    var grade: Char = if(score >= 90.0)
        'A'
    else if(score in 80.0 .. 89.9)
        'B'
    else if(score in 70.0 .. 79.9)
        'C'
    else
        'D'

    println("Score: $score Grade: $grade")
  }
```
<br>
앞에서는 else if 문의 분기가 4개 등급일 경우였습니다. 하지만 만약 분기가 더 많아지면 코드가 길어지고 복잡해집니다. 코틀린에서는 when문을 통해서 아래와 같이 간결하게 수행 가능합니다.  
```kotlin
  fun main(){
    print("Enter the score: ")
    val score = readLine()!!.toDouble()

    var grade: Char = when {
      score >= 90.0 -> 'A'
      score in 80.0 .. 89.9 -> 'B'
      score in 70.0 .. 79.9 -> 'C'
      else -> 'D'
    }

    println("Score: $score Grade: $grade")
  }
```
<br>
when문은 인자를 넣어 *when(score)* 표현해도 가능하고, 위 처럼 인자를 넣지 않아도 됩니다. 화살표 기호에 따라 실행을 어떻게 할건지 구성할 수 있습니다. 처음 코드보다 훨씬 간결해졌죠?  
------------------------  

## 반복문  
반복문은 java와 같습니다. 반복문은 for, while, do while문을 사용하여 반복해야할 작업을 조건에 따라 실행합니다. 다만 코틀린에서는 위에서 배웠단 범위 연산자를 사용 가능하여 범위 조건에 대해서는 간결하게 표현 가능합니다. 하나의 예시를 표현하면 아래와 같습니다.   
```kotlin
  fun main() {
    do {
        print("Enter an integer: ")
        val input = readLine()!!.toInt()

        for (i in 0 .. (input-1)) {
            for(j in 0..(input-1)) print((i + j) % input +1)
            println()
        }

    } while (input != 0)
  }
```
>Enter an integer: 5  
12345  
23451  
34512  
45123  
51234  
Enter an integer: 0  
Process finished with exit code 0

readLine()으로 입력값을 받고 숫자를 순서대로 나열하고 하나씩 자리를 옮겨가며 반복합니다. 그리고 input이 0이되면 while 조건식이 맞지 않아 빠져나오게 됩니다.  

------------------------  

## 마치며
코틀린의 흐름 제어 중 크게 반복문과 조건문을 알아보았습니다. 그 외에도 continue, break, try catch, 등 예외 처리나 다른 흐름 제어문에 대해서도 알고 있어야합니다. 이 내용은 java와 크게 다르지 않아 다루지 않았습니다.  