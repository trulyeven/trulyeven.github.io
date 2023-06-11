---
title : "[JAVA] Tesseract OCR spring 세팅"
date : 2023-06-11 00:00:00 +0900 # +/-TTTT
categories : [JAVA, spring]
tags : [java, spring, selenium] #소문자만 가능
---

# 1. 환경
- windows 11
- java JDK 17
- springboot 3.11
- MS edge

# 2. selenium

웹 크롤링(crawling), 웹 스크랩핑(Scraping)을 하는 데 사용되는 라이브러리

- 빅데이터관련, 동적인 자료를 수집할 때 주로 사용한다
- 브라우저 드라이버를 사용하여 동적 데이터도 수집 가능하다
- Jsoup에 비해 속도는 느리다 

Jsoup
: HTTP Request를 사용하여 정적으로 자료를 수집하는 라이브러리

# 3. Web Driver

여기서는 Microsoft Edge 브라우저를 사용하여 selenium을 실행한다
다른 브라우저의 경우 알맞는 브라우저 드라이버를 설치하면 된다

먼저 자신의 브라우저의 버전을 확인한다
![image](https://github.com/trulyeven/vocr/assets/113951017/7f0e9d6d-9509-43af-ac05-386b07dbe2f3)
{w:300}


[Edge driver 다운로드 사이트](https://developer.microsoft.com/ko-kr/microsoft-edge/tools/webdriver/)


참고

[tesseract github 페이지](https://github.com/tesseract-ocr/tessdoc#tesseract-user-manual)  
[tess4j.sourceforge.net](https://tess4j.sourceforge.net/)
