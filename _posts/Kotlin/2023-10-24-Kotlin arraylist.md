---
title : "[Kotlin] arrayList"
date : 2023-10-24 00:00:00 +0900 # +/-TTTT
categories : [kotlin]
tags : [kotlin, array, list, arraylist] #소문자만 가능
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

[list 바로가기](https://trulyeven.github.io/posts/Kotlin-list/)


## 3. arrayList

배열의 크기가 유동적이고 값을 수정할 수 있다

현재 kotlin의 ArrayList는 MutableList 인터페이스를 상속받은 구현체이다

따라서 arrayList와 mutableList 둘 다 작동 원리는 대부분 같다

## 3.1. arrayList 생성

```kotlin
val arrayList = arrayListOf(1, 2, 3)  // 1 2 3

var arr = ArrayList<Any> ()  // 비어있는 arrayList
```

---

## 3.2. arrayList 접근

```kotlin
val arr = arrayListOf("가","나","다","라")

// 인덱싱
arr[0]  // 가
arr[3]  // 라

// 슬라이싱
// - 첫번째 인덱스부터 두번째 인덱스 전까지
arr.subList(1, 3)  // [나, 다]
```

## 3.2. arrayList 출력

```kotlin
val lst = listOf(3, 4, 5)
print(lst)  // [3, 4, 5]
```

list와 마찬가지로 print를 사용해 직접 출력이 가능하다


---

참고자료

[kotlin collections 공식문서](https://kotlinlang.org/api/latest/jvm/stdlib/kotlin.collections/)

---
