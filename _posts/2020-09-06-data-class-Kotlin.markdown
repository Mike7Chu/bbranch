---
layout: post
title:  "코틀린(Kotlin) 제네릭 -11-"
date:   2020-09-06 22:20:22 +0900
image:  Kotlin-logo.png
tags:   [Kotlin]
---
## Overview  
제네릭이란 컴파일 타임에 인스턴스의 자료형을 결정하여 안정성을 높이고 형변환의 번거로움을 줄여줍니다.  
<span style="color: grey">*이 글은 "Do it! 코틀린 프로그래밍"을 읽으면서 작성되었습니다.*</span>  
<br>
[1. 제네릭](#제네릭)  
[2. 마치며](#마치며)  

------------------------  

## 제네릭  
제네릭은 **\<\>** 브라켓 사이에 형식 매개변수를 넣어 선언하여 이때 매개변수 형식을 결정할 수 있습니다.여러 자료형을 다루어야 하는 **List, Set, Map**등에서 많이 사용됩니다. 의도하지 않은 자료형의 객체를 지정하는 것을 막고 객체를 사용할 때 원래의 자료형에서 다른 자료형으로 형 변화 ㄴ시 발생할 수 있는 오류를 줄어줍니다. 아래 예제에서 살펴보겠습니다.    
```kotlin
class Box<T>(t: T) {
    var name = t
}

fun main() {
    var box1: Box<Int> = Box<Int>(1)
    var box2: Box<String> = Box<String>("Hello")
    println(box1.name)
    println(box2.name)
}
```
>1  
Hello  

<br>
Box<T>에서 T가 바로 형식 매개변수 이름입니다. 그에 따라 box1에는 정수형 타입이 box2에는 문자열 타입이 된 것으로 알 수 있습니다. 여기서 T의 경우 형식을 말하며 그 외에도 다른 규칙을 줄 수 있습니다. 다른 규칙은 아래 표와 같습니다.  

|형식 매개변수 이름|의미|  
|--------|--------|  
|E|요소(Element)|  
|K|키(key)|  
|N|숫자(Number)|  
|T|형식(Type)|  
|V|값(Value)|  
|S,U,V,etc|두 번째, 세 번째, 네 번째 형식(2nd, 3rd, 4th types)|  

------------------------  

## 마치며
읽어주셔서 감사합니다.  
