---
layout: post
title:  "코틀린(Kotlin) 추상클래스 -8-"
date:   2020-08-09 22:30:22 +0900
image:  Kotlin-logo.png
tags:   [Kotlin]
---
## Overview  
추상클래스를 정리하겠습니다.  
<span style="color: grey">*이 글은 "Do it! 코틀린 프로그래밍"을 읽으면서 작성되었습니다.*</span>  
<br>
[1. 추상클래스](#추상클래스)  
[2. 마치며](#마치며)  

------------------------  

## 추상클래스  
추상클래스는 무엇일까요? 추상클래스는 말그대로 추상적인 클래스로 구체화되지 않은 클래스라고도 할 수 있습니다. 추상클래스는 설계와 같다고 책에서는 소개하고 있습니다. 제가 이해하였을 때는, 모듈화의 특성을 더 가지기 위해서 공통의 특징을 구현하고자 할 때, 사용하는 것이 추상클래스로 이해하고 있습니다. 이런 추상클래스를 하위클래스에서 상속하여, 객체를 생성합니다. 예를 들면 '차'라는 추상클래스로 '벤츠' '소나타' 'BMW'라는 하위클래스를 만드는 것을 들 수 있겠습니다.  
```kotlin
abstract class Vehicle(val name: String, val color: String, val weight: Double) {
    abstract var maxSpeed: Double
    var year = "2018"

    abstract fun start()
    abstract fun stop()

    fun displaySpecs() {
        println("Name: $name, Color: $color, Weight: $weight, Year: $year, Max Speed: $maxSpeed")
    }
}

class Car(name: String,
         color: String,
         weight: Double,
         override var maxSpeed: Double)
    : Vehicle(name, color, weight) {

    override fun start() {
        println("Car Started")
    }

    override fun stop() {
        println("Car Stopepd")
    }
}

class Motorcycle(name: String,
          color: String,
          weight: Double,
          override var maxSpeed: Double)
    : Vehicle(name, color, weight) {

    override fun start() {
        println("Bike Started")
    }

    override fun stop() {
        println("Bike Stopepd")
    }
}

fun main() {
    val car = Car("SuperMatiz", "yellow", 1110.0, 270.0)
    val motor = Motorcycle("DreamBike", "red", 173.0, 100.0)

    car.year = "2013"

    car.displaySpecs()
    car.start()
    motor.displaySpecs()
    motor.start()
}
```
>Name: SuperMatiz, Color: yellow, Weight: 1110.0, Year: 2013, Max Speed: 270.0  
Car Started  
Name: DreamBike, Color: red, Weight: 173.0, Year: 2018, Max Speed: 100.0  
Bike Started   

<br>
Vehicle 추상클래스에서 Car와 Motorcycle이라는 하위클래스를 생성하여 호출하는 예제입니다. abstract키워드를 쓰면 추상클래스, 프로퍼티, 메소드를 선언할 수 있습니다. abstract키워드를 쓰면 자동으로 open 되며 open 키워드 없이 오버라이딩이 가능합니다.  

------------------------  

## 마치며
읽어주셔서 감사합니다.  