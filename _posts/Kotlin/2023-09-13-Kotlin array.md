---
title : "[Kotlin] array, list, arrayList"
date : 2023-09-13 00:00:00 +0900 # +/-TTTT
categories : [kotlin]
tags : [kotlin, array, list] #소문자만 가능
math : true
# mermaid : false
image:                         # 미리보기 이미지
  path: https://i.namu.wiki/i/SyEg6ArvrsKDsWVBweN4PPxtoxFIaboI9_zceYTL5FcGUBms0nDyfYldaRhUG_ToIQ6MftttN9Pku_-T4FgLcXAHFj8I_9rEIL55fOMCYe9R47MwtqjKocwe8XT9DqOMT4tceiUC2JzvYNrdtBBCRA.svg
  width: 1000                  # in pixels
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


## 1. array

Array는 메모리에서 연속적인 공간을 차지하는 정적인 자료구조이다

연속적인 공간을 차지하므로, Index를 이용한 빠른 접근이 가능하다

Array의 경우에는 선언 당시에 배열의 크기가 정해지고 조절이 불가능하다


### array 생성

> var 배열이름: Array<배열 값의 타입> = arrayOf<배열 값의 타입>(값, ...)
> var 배열이름: Array<배열 값의 타입> = Array<배열 값의 타입>(배열의 크기) { init -> T }

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

`<Any>`로 여러 자료형을 넣을 수 있다(생략가능)

IntRange는 바로 Array로 변환하지 못하므로 List로 변환 후에 Array로 변환시켜야 한다

---

#### emptyArray()

```kotlin
val emptyArray = emptyArray<Int>()
```

빈 배열을 생성한다, 타입을 지정해줘야 한다

---

#### arrayOfNulls()

```kotlin
var nullArr = arrayOfNulls<Int>(3) // null,null,null
```

null 배열을 생성시에는 타입을 지정해줘야 한다

Array의 크기 값(size)을 지정하면 그만큼 null이 들어간 배열을 생성한다

---

### array 접근 및 함수

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

```kotlin
// 배열 출력
// forEach {}
arr.forEach { print({ it }) }  // 100200300Hi
// 배열.contentToString()
println(arr.contentToString())   // [100, 200, 300, Hi]
// 배열.joinToString(문자열)
println(arr.joinToString("*"))   // 100*200*300*Hi
```

.plus()
```kotlin
var array1 = arrayOf(1, 2, 3)
array1 = array1.plus(4)  // 1 2 3 4
```

---

<br><br>

## list

코틀린의 List는 기본적으로 immutable으로 읽기 전용으로 배열안의 내용을 수정할 수 없다

하지만 mutable로 선언할 경우 값을 변경할 수 있다

val로 초기화할 경우 재할당은 불가능하지만 추가,삭제 등은 가능하다

### list 생성

```kotlin
val lst1 = listOf(0, 1, 2)
val lst2 = List(3,  {i -> i})

// mutable로 생성
val lst3 = mutableListOf<Int>(0, 1, 2)
val lst4 = MutableList<Int>(3, {i -> i})
```

---

### list 접근 및 함수

수정,삭제 메소드는 mutableList만 가능하다

.add()
```kotlin
val mlst = mutableListOf<Int>(0, 1, 2)
val lst = listOf<Int>(7, 8, 9)

mlst.add(3)    // 0 1 2 3
// 1번 idx에 6 추가
mlst.add(1, 6) // 0 6 1 2

// 기존 list에 list2의 값들을 더한다.
mlst.addAll(lst)   // 0 1 2 7 8 9
mlst.addAll(2, lst) // 0 1 7 8 9 2
```

.remove()
```kotlin
val mlst = mutableListOf<Int>(1 ,2 ,3) // 1 2 3
val lst = listOf<Int>(2, 3, 4)         // 2 3 4
mlst.remove(2) // 1 3
mlst.removeAt(0) // 2 3    1번 인덱스 제거

// lst와 공집합 제거
mlst.removeAll(lst)  // 1

lst.clear()  // 리스트 비우기
```
remove는 해당 값을 찾아 삭제하고 true를 반환한다

해당하는 값이 없으면 false를 반환한다

.retainAll()
```kotlin
val mlst = mutableListOf<Int>(1 ,2 ,3) // 1 2 3
val lst = listOf<Int>(2, 3, 4)         // 2 3 4

mlst.retainAll(lst)  // 2 3
```

두 리스트의 공집합
```kotlin
val mlst = mutableListOf<Int>(1 ,2 ,3, 4)

mlst.subList(1, 3)  // 2 3
```

---

<br><br>

## arrayList

배열의 크기가 유동적이고 값을 수정할 수 있다

현재 kotlin의 ArrayList는 MutableList 인터페이스를 상속받은 구현체이다

따라서 arrayList와 mutableList 둘 다 작동 원리는 같다

### arrayList 생성

```kotlin
val arrayList = arrayListOf(1, 2, 3)  // 1 2 3
```


---

[kotlin collections 공식문서](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/)

---

