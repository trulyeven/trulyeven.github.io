---
title : "[Kotlin] list"
date : 2023-10-24 00:00:00 +0900 # +/-TTTT
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

[array 바로가기](https://trulyeven.github.io/posts/Kotlin-array/)

[arraylist 바로가기](https://trulyeven.github.io/posts/Kotlin-arraylist/)


## 1. list

코틀린의 List는 기본적으로 immutable으로 읽기 전용으로 배열안의 내용을 수정할 수 없다

하지만 mutable로 선언할 경우 값을 변경할 수 있다

val로 초기화할 경우 재할당은 불가능하지만 추가,삭제 등은 가능하다

## 2. list 생성

```kotlin
val lst1 = listOf(0, 1, 2)
val lst2 = List(3,  {i -> i})

// mutable로 생성
val lst3 = mutableListOf<Int>(0, 1, 2)
val lst4 = MutableList<Int>(3, {i -> i})
```

---

## 3. list 접근
```kotlin
val lst = listOf(3, 4, 5)

// 인덱싱
lst[0]  // 3

// 슬라이싱
lst.subList(1, 3) // [4, 5]
```


## 4. list 출력
```kotlin
val lst = listOf(3, 4, 5)
print(lst)  // [3, 4, 5]
```

list는 print를 사용해 직접 출력이 가능하다

## 5. list 함수

수정,삭제 함수는 `mutableList`만 가능하다

---

### 5.1. add()
: list에 값 추가

```kotlin
val mlst = mutableListOf<Int>(0, 1, 2)
val lst = listOf<Int>(7, 8, 9)

mlst.add(3)    // 0 1 2 3
// 1번 index에 6 추가
mlst.add(1, 6) // 0 6 1 2


mlst.addAll(lst)   // 0 1 2 7 8 9
// 2번 index에 추가
mlst.addAll(2, lst) // 0 1 7 8 9 2
```

### 5.2. remove()
: list에 값 제거(index 기준)

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

### 5.3. clear()
: list 모든 값 제거

```kotlin
lst.clear()  //
```


### 5.4. retainAll()
: 두 리스트의 공집합

```kotlin
val mlst = mutableListOf<Int>(1 ,2 ,3) // 1 2 3
val lst = listOf<Int>(2, 3, 4)         // 2 3 4

mlst.retainAll(lst)  // 2 3
```


### 5.5. subList()
: 두 인덱스값 사이으로 부분 리스트

```kotlin
val mlst = mutableListOf<Int>(1 ,2 ,3, 4)

mlst.subList(1, 3)  // 2 3
```

---

참고자료

[kotlin collections 공식문서](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/)

---
