---
layout: post
title:  "코틀린(Kotlin) 컬렉션(List)-12-"
date:   2020-09-20 21:30:22 +0900
image:  Kotlin-logo.png
tags:   [Kotlin]
---
## Overview  
표준 라이브러리로 제공되고 있는 자료구조 중 컬렉션을 알아보겠습니다. 컬렉션은 List, Set, Map등이 있습니다. 컬렉션에 대해서 알아보겠습니다.  
<span style="color: grey">*이 글은 "Do it! 코틀린 프로그래밍"을 읽으면서 작성되었습니다.*</span>  
<br>
[1. Collection](#Collection)  
[2. List](#List)  
[2. 마치며](#마치며)  

------------------------  

## Collection  
컬렉션은 불변형(immutable)과 가변형(mutable)으로 나누어집니다. 자바에서는 오로지 가변형만 취급되므로, 자바코드와 같이 작성할 경우 주의해야합니다.  

|컬렉션|불변형|가변형|  
|--------|--------|--------|  
|List|listOf|mutableListOf, arrayListOf|  
|Set|setOf|mutableSetOf, hashSetOf, linkedSetOf, sortedSetOf|  
|Map|mapOf|mutableMapOf, hashMapOf, linkedMapOf, sortedMapOf|  

<br>
또한, 변수를 선언할 때 불변형 val의 사용을 권장하듯이, 컬렉션도 되도록이면 읽기 전용인 불변형을 선언할 것을 권장합니다. 이제 하나씩 살펴보도록 하겠습니다.  

------------------------  

## List  
List는 불변형일 경우 listOf()함수를 사용하여야 하며 원형은 다음과 같습니다.  
```kotlin
public fun <T> listOf(vararg elements: T): List<T>
```
<br>
값을 반환할 때는, List<T>로 반환하며 <T> 라는 형식 매개변수를 가져 원하는 자료형을 지정할 수 있습니다.  
```kotlin
fun main() {//do it Kotlin chap09.section2
    var numbers: List<Int> = listOf(1, 2, 3, 4, 5)
    var names: List<String> = listOf("one", "two", "three")

    for (name in names) {
        println(name)
    }
    for (num in numbers) print(num)
    println()
}
```
>one  
two  
three  
12345  

<br>
List에 접근할 위 처럼 in을 통해서 각각 변수를 받아 처리도 가능하고, 다음과 같이 인덱스를 지정해서 접근이 가능합니다.  
```kotlin
for(index in names.indices) {//인덱스 지정
    println("names[$index] = $(names[index])")
}
```
>names[0] = one  
>names[1] = two  
>names[2] = three  

위와 같이 index를 통해 얻을 수 있습니다.  
<br>
### emptyList(), listOfNotNull()  
비어있는 List를 생성하려면 다음과 같이 선언할 수 있습니다.
```kotlin
val emptyList: List<String> = emptyList<String>()
```
<br>
만약 null을 제외하고 초기화 하려면 다음과 같이 초기화 할 수 있습니다.  
```kotlin
val nonNullsList: List<Int> = listOfNotNull(2, 45, 2, null, 5, null)
println(nonNullsList)
```
>[2, 45, 2, 5]  

List는 다음과 같은 메서드를 멤버로 가지고 있습니다.  

|멤버 메서드|설명|  
|--------|--------|  
|get(index: Int)|특정 인덱스를 인자로 받아 해당 요소를 반환한다.|  
|indexOf(element: E)|인자로 받은 요소가 첫 번째로 나타나는 인덱스를 반환하며, 없으면 -1을 반환한다.|  
|lastIndexOf(element: E)|인자로 받은 요소가 마지막으로 나타나는 인덱스를 반환하고, 없으면 -1을 반환한다.|  
|listIterator()|목록에 있는 iterator를 반환한다.|  
|subList(fromIndex: Int, toIndex: Int)|특정 인덱스의 from과 to 범위에 있는 요소 목록을 반환한다.|  

<br>
### 가변현 List 생성하기  
가변형 List를 생성하려면 두가지 헬퍼 함수를 사용하여 생성가능합니다.(**arrayListOf(), mutableListOf()**)  
```kotlin
public fun <T> arrayListOf(vararg elements: T): ArrayList<T>
public fun <T> mutableListOf(vararg elements: T): MutableList<T>
```
다만 이 둘의 차이점은 arrayListOf()의 경우 자료형이 List가 아닌 자바의 ArrayList를 반환합니다. mutableListOf()의 경우 MutableList Type 입니다. MutableList는 ArrayList와 동작상 같고 명시적으로 의미상 차이만 있다고 합니다. 실제 구현은 다음과 같이 할 수 있습니다.  
```kotlin
fun main() {
    val mutableList: MutableList<String> = mutableListOf<String>("Kildong", "Dooly", "Chelsu")
    mutableList.add("Ben")
    mutableList.removeAt(1)
    mutableList[0] = "Sean"
    println(mutableList)

    val mutableListMixed = mutableListOf("Android", "Apple", 5, 6, 'X')
    println(mutableListMixed)

}
```
>[Sean, Chelsu, Ben]  
>[Android, Apple ,5, 6, X]  

<br>
add, removeAt 과 같은 가변형용 멤버 메소드를 사용할 수 있습니다. 가변형에서 사용할 수 있는 메소드는 다음과 같습니다.  

|멤버 메서드|설명|  
|--------|--------|  
|add(index: Int)|인자로 전달 받은 요소를 추가하고 true를 반환하며, 이미 요소가 있거나 중복이 허용되지 않으면 false를 반환한다.|  
|remove(element: E)|인자로 전달 받은 요소를 삭제하고 true를 반환하며, 삭제하려는 요소가 없다면 false를 반환한다.|  
|addAll(element: Collection<E>)|컬렉션을 인자로 전달 받아 모든 요소를 추가하고 true를 반환하며, 실패하면 false를 반환한다.|  
|removeAll(element: Collection<E>)|컬렉션을 인자로 전달 받아 모든 요소를 삭제하고 true를 반환하며, 실패하면 false를 반환한다.|  
|retainAll(element: Collection<E>)|인자로 전달 받은 컬렉션의 요소만 보유한다. 성공하면 true를 반환하고, 실패하면 false를 반환한다.|  
|clear())|컬렉션의 모든 요소를 삭제한다.|  

------------------------  

## 마치며
읽어주셔서 감사합니다.  
