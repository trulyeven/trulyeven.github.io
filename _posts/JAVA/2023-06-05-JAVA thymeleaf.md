---
title : "[JAVA] Thymeleaf 사용법"
date : 2023-06-05 00:00:00 +0900 # +/-TTTT
categories : [JAVA, spring]
tags : [java, spring, python, thymeleaf] #소문자만 가능
---

# 1. Thymeleaf란?
> JSP, Thymeleaf, Mustache 같은 템플릿 엔진 중 하나
  View Template(뷰 템플릿), 컨트롤러가 전달하는 데이터를 이용하여 동적으로 화면을 구성할 수 있다.
  html태그를 기반으로하여 `th:속성`을 이용하여 동적인 View를 제공


![error](https://github.com/trulyeven/trulyeven.github.io/assets/113951017/9c5500f6-6cc5-4b9b-9d76-5c4c3a6e26f4)
: thymeleaf 문법 오류일 경우 자주보게되는 페이지

---

# 2. Thymeleaf 사용하기
spring에서 thymeleaf를 사용하기 위해서는 Dependency에 thymeleaf를 추가해준다

## 2.1 Dependency

### 2.1.1 Gradle
`build.gradle`
```
implementation 'org.springframework.boot:spring-boot-starter-thymeleaf'
```

### 2.1.2 Maven
`pom.xml`
```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-thymeleaf</artifactId>
</dependency>
```

---

## 2.2 기본경로 확인(spring)
> 프로젝트 폴더(root) / src / main / resources / templates
  하위 폴더의 html도 사용가능

### 2.2.1 application.yml
```
# Thymeleaf
spring:
  thymeleaf:
    prefix: classpath:templates/thymeleaf/         <- 기본 경로 설정
    check-template-location: true
    suffix: .html
    mode: HTML
    cache: false                          <- default true, 개발 시에는 false로 두면
                                                  캐시 기능 없어서 변경이 바로 반영됨
```

## 2.2.2 html 설정

```
<html lang="en" xmlns:th="http://www.thymeleaf.org">
```
> html 태그에 추가

---

# 3. Themeleaf 문법

```html
<input type="text" value="aaa" th:value="${bbb}">
<!-- bbb가 존재하면 th:value가 value를 대체함 -->
```
> `th:속성` 값이 존재하면 타임리프 문법을 우선시함

---

## 3.1 ${ }
```html
<div th:text="${data}"></div>
<div th:utext="${data}"></div>  // 값에 html 태그가 있으면 태그를 인식 
<div>[[ ${data} ]]</div>
```
컨트롤러에서 전달받은 데이터 접근  
전달받은 값이 <h2>Hello!</h2> 라면  
th:text  -> <h2>Hello!</h2>  
th:utext -> Hello! &nbsp;&nbsp;&nbsp; #h2 태그 적용됨

---

## 3.2 @{ }
```html
<a th:href="@{이동할 url}"></a>
```
`<a>` 태그 href와 동일

---

## 3.3 th:value
```html
<input type="text" id="userId" th:value="${userId}"/>
```
input, button 태그 등에 value를 넣을 때 사용

---

## 3.4 Form 태그 (th:action, th:object, th:field)
```html
<form th:action="@{/login}" th:object="${loginForm}" method="post">
    <input type="text" id="userId" th:field="*{userId}" >
    <input type="password" id="userPw" th:field="*{userPw}" >
</form>
```

- th:action
  + `<form>` 태그 사용시, 해당 경로로 요청을 보낼 때 사용

- th:object
  + `<form>` 태그에서 Submit을 할 때 데이터가 `th:object` 속성을 통해 지정한 객체에 값을 담아 넘긴다.

- th:field
  + `th:object`속성과 함께 `th:field`를 이용해서 HTML 태그에 멤버 변수를 매핑할 수 있다.
  + `th:object`와 `th:field`는 Controller에서 특정 클래스의 객체를 전달 받은 경우에만 사용 가능하다.

---

## 3.5 th:with
```html
<div th:with="var=${val}" th:text="${var}">
```
변수 값을 지정하여 사용

---

## 3.6 th:switch
```html
<div th:switch="${val}">
    <p th:case="abc">
    <p th:case="${#authentication.name}">
    <p th:case="*">   // java switch-case의 default
</div>
```
Swith-case문을 사용

---

## 3.7 th:if 
```html
<th:block th:if="${val >= 2}">
  <span>123456</span>  // if 조건이 True 일 경우
</th:block>
<th:block th:unless="${val == 1}">  // th:unless는 else
  <span>abcdefg</span>  // else 조건이 true일 경우
</th:block>
```

---

## 3.8 th:each
```html
<tr th:each="val : ${valList}">
		<td th:text="${val.seq}"></td>
		<td th:text="${val.name}"></td>
</tr>
```
valList의 값을 다 꺼낼 때까지 <tr> 태그 반복

### 3.8.1 #numbers.sequence()
```html
<th:block th:each="num : ${#numbers.sequence(1,5)}">
	<div th:text="${num}"></div>
</th:block>
```
1~5 까지 반복

### 3.8.2 status 변수

th:each 사용하면 상태를 추적할 수 있는 status 변수를 제공해줌
```html
<div th:text="${numStat.index}"> </div>
<!-- 
index   : 현재 인덱스(0부터)		
count   : 현재 반복 수(1부터)	
size  	: 총 반복 횟수
current :	현재 요소
even    : 현재 반복이 짝수인지(boolean) 
odd     : 현재 반복이 홀수인지(boolean)
first   : 현재 반복이 첫번째인지(boolean) 
last    : 현재 반복이 마지막인지(boolean)
 -->
```


---

참고
[themeleaf 공식 document](https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf.html#using-texts/)