---
layout: post
title:  "코틀린(Kotlin) 컬렉션(Set, Map)-13-"
date:   2020-09-27 18:21:22 +0900
image:  Kotlin-logo.png
tags:   [Kotlin]
---
## Overview  
지난 시간에 이어서 컬렉션인 Set, Map을 다루겠습니다.  
<span style="color: grey">*이 글은 "Do it! 코틀린 프로그래밍"을 읽으면서 작성되었습니다.*</span>  
<br>
[1. Set](#Set)  
[2. Map](#Map)  
[2. 마치며](#마치며)  

------------------------  

## Set  
Set의 경우 List와 달리 순서가 없는 집합입니다. Set의 경우 집합 개념이기 때문에, 값을 중복해서 가질 수 없는 차이가 있습니다. 따라서 모든 요소가 유일합니다. Set은 List와 마찬가지로 **setOf()**로 불변형을 생성하고 **mutableSetOf()**로 가변형을 생성할 수 있습니다.  

<br>
또한, 변수를 선언할 때 불변형 val의 사용을 권장하듯이, 컬렉션도 되도록이면 읽기 전용인 불변형을 선언할 것을 권장합니다. 이제 하나씩 살펴보도록 하겠습니다.  
```kotlin
//불변형 Set 예제
fun main() {//do it Kotlin chap09.section3
    val mixedTypeSet = setOf("Hello", 5, "world", 3.14, 'c')
    var intSet: Set<Int> = setOf<Int>(1, 5, 5)

    println(mixedTypeSet)
    println(intSet)
}
```
>[Hello, 5, world, 3.14, c]  
[1, 5]  

<br>

```kotlin
//가변현 Set예제
fun main() {//do it Kotlin chap09.section3
    val animals = mutableSetOf("Lion", "Dog", "Cat", "Python", "Hippo")

    println(animals)
    
    animals.add("Dog")
    println(animals)

    animals.remove("Python")
    println(animals)
}
```
>[Lion, Dog, Cat, Python, Hippo]  
[Lion, Dog, Cat, Python, Hippo]  
[Lion, Dog, Cat, Hippo]  

------------------------  

Set에서는 업데이트를 하려면 add()와 remove()를 통해서 할 수 있습니다. Dog를 추가하려면 중복 되기 때문에 추가 안되는 것을 알 수 있습니다.  

### hashSetOf()  
hashSetOf()는 자바의 hashSet컬렉션을 생성하는 함수입니다. 이는 해시 테이블을 이용하여 내부의 키와 인덱스를 이용하여 검색과 변경을 빠르게 처리할 수 있는 자료구조 입니다. HashSet은 불변성 선언이 없습니다.  
```kotlin
//HashSet예제
fun main() {//do it Kotlin chap09.section3
    val intsHashSet: HashSet<Int> = hashSetOf(6, 3, 4, 7)
    intHashSet.add(5)
    intHashSet.remove(6)
    println(intsHashSet)
}
```
>[3, 4, 5, 7]  
<br>

HashSet은 Set이기 때문에 중복된 겂은 무시합니다. 추가로 따로 정렬 기능은 없지만 Hash기능으로 값을 찾을 때 O(1) 상수 시간을 가지게 됩니다.  

### sortedSetOf()  
sortedSetOf()함수는 자바의 TreeSet 컬렉션을 정렬된 상태로 반환 합니다. 이 함수를 사용하려면 java.util.* 패키지를 임포트 해야합니다. Tree구조는 HashTable과 달리 검색과 정렬에 있어서 일정한 시간을 소모하는 장점이 있습니다.  
```kotlin
//가변현 Set예제
import java.util.*

fun main() {//do it Kotlin chap09.section3
    val intsSortedSet: TreeSet<Int> = sortedSetOf(4, 1, 7, 2)

    intsSortedSet.add(6)
    intsSortedSet.remove(1)
    println("intsSortedSet = ${intsSortedSet}")

    intsSortedSet.clear()
    println("intsSortedSet = ${intsSortedSet}")
}
```
>intsSortedSet = [2, 4, 6, 7]  
intsSortedSet = []  
<br>

### linkedSetOf()  
linkedSetOf()의 경우 링크드리스트를 사용해 해시 테이블에 요소를 사용합니다. 링크드 리스트는 저장된 순서에 따라 값이 정렬되며 앞에 언급 된 두 자료구조보다 느립니다. 다만 자료구조상 데이터를 가리키는 포인터 연결을 통해 메모리 저장 공간을 더 효율적으로 사용할 수 있습니다.  
```kotlin
//가변현 Set예제
fun main() {//do it Kotlin chap09.section3
    val intsLinkedHashSet: java.util.intsLinkedHashSet<Int> = linkedSetOf(35, 21, 76, 26, 75)
    intsLinkedHashSet.add(4)
    intsLinkedHashSet.remove(21)

    println(intsLinkedHashSet)
    intsLinkedHashSet.clear()
    println(intsLinkedHashSet)
}
```
>[35, 76, 26, 75, 4]
[] 
<br>

---------------

## Map


------------------------  

## 마치며
읽어주셔서 감사합니다.  
