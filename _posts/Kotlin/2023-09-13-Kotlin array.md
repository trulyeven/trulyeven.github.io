---
title : "[Kotlin] array"
date : 2023-09-13 00:00:00 +0900 # +/-TTTT
categories : [kotlin]
tags : [kotlin, array, list] #소문자만 가능
math : true
# mermaid : false
image:                         # 미리보기 이미지
  path: https://github.com/trulyeven/trulyeven.github.io/assets/113951017/f75671d4-afc0-4eb0-850d-4e1d5d76f2cb
  width: 700                  # in pixels
  height: 400                  # in pixels
  alt: kotlin
---

[play.kotlinlang.org](https://play.kotlinlang.org/)

코틀린 코드를 연습해볼 수 있는 공식사이트

---

> kotlin v1.9.10 으로 작성됨


Collection에는 List, Map, Set 등이 있다
Collection은 크게 Mutable과 immutable으로 구분된다

> Mutable - read & write
> immutable - read only

[list 바로가기](https://trulyeven.github.io/posts/Kotlin-list/)

[arraylist 바로가기](https://trulyeven.github.io/posts/Kotlin-arraylist/)


## 1. array

Array는 메모리에서 연속적인 공간을 차지하는 정적인 자료구조이다

연속적인 공간을 차지하므로, Index를 이용한 빠른 접근이 가능하다

Array의 경우에는 선언 당시에 배열의 크기가 정해지고 조절이 불가능하다


## 2. array 생성

> var 배열이름: Array\<배열 값의 타입\> = arrayOf\<배열 값의 타입\>(값, ...)
>
> var 배열이름: Array\<배열 값의 타입\> = Array\<배열 값의 타입\>(배열의 크기) { init -> T }

선언 때 크기를 지정 후, 배열의 크기를 변경 할 수 없다

```kotlin
var array1 = arrayOf(100, 200, 300, "Hi")       // 선언과 동시에 데이터 넣기
var array2 = arrayOf<String>("100", "b", "hi")  // 타입 지정

var arr1 = Array(5) { i -> 0 }          // 0,0,0,0,0
var arr2 = Array(5) { index -> index }  // 0,1,2,3,4

// IntRange를 이용하여 array 생성
val intArray: = (0..3).toList().toTypedArray()  // 0,1,2,3
```

코틀린에서는 arrayOf() 를 사용해 타입과 크기를 생략 가능하다

IntRange는 바로 Array로 변환하지 못하므로 List로 변환 후에 Array로 변환시켜야 한다

---

### 2.1. emptyArray()

```kotlin
val emptyArray = emptyArray<Int>()

val emptyStrArray: Array<String> = arrayOf() // 빈 배열
```

빈 배열을 생성한다, 타입을 지정해줘야 한다

---

### 2.2. arrayOfNulls()

```kotlin
var nullArr = arrayOfNulls<Int>(3) // null,null,null
```

null 배열을 생성시에는 타입을 지정해줘야 한다

Array의 크기 값(size)을 지정하면 그만큼 null이 들어간 배열을 생성한다

---

## 3. array 접근

```kotlin
var arr = arrayOf(100, 200, 300, "Hi")  

// 배열 접근 및 조작
arr[0]          // 100
arr[1] = 201    // 200 → 201
arr.get(0)       // 100
arr.set(2, "c")  // 300 → "c"

// 배열.indexOf(100) : 해당 값의 첫번째 인덱스, 없으면 -1
arr.indexOf(100)  // 0

// 배열.contentEquals(배열) : 배열끼리 비교
arr.contentEquals(arr)  // true
```

---

## 4. array 출력

```kotlin
// forEach {}
arr.forEach { print({ it }) }  // 100200300Hi

// 배열.contentToString()
println(arr.contentToString())   // [100, 200, 300, Hi]

// 배열.joinToString(문자열)
println(arr.joinToString("*"))   // 100*200*300*Hi
```

## 5. array 함수

### plus()
값을 추가하여 새로운 배열 생성

```kotlin
var array1 = arrayOf(1, 2, 3)
var array2 = array1.plus(4)  // 1 2 3 4
```

---

참고자료

[kotlin collections 공식문서](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/)

---
