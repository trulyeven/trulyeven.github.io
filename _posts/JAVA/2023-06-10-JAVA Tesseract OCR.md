---
title : "[JAVA] Tesseract OCR spring 세팅"
date : 2023-06-10 00:00:00 +0900 # +/-TTTT
categories : [JAVA, spring]
tags : [java, spring, tesseract, OCR] #소문자만 가능
---

# 1. 환경
- windows 11
- java JDK 17
- springboot 3.11

# 2. Tesseract

Tesseract는 Apache 2.0 라이선스에 따라 사용할 수 있는 오픈 소스 텍스트 인식(OCR) 엔진이다.  
메인 버전인 Tesseract 5는 현재 안정적인 버전이며 5.0.0은 2021.11.30에 release되었다.
이를 활용해서 spring에 OCR을 구현하는 예제를 만들어보겠다.

OCR(Optical Character Recognition)
: 광학 문자 인식을 일컫는다.
  사람이 쓰거나 기계로 인쇄한 문자의 영상을 이미지 스캐너로 획득하여 기계가 읽을 수 있는 문자로 변환하는 기술

## Tesseract 설치

[Tesseract 다운로드 페이지](https://github.com/UB-Mannheim/tesseract/wiki)

windows 설치 페이지이므로 다른 운영체제는 tesseract 페이지에서 찾아주면 된다

![image](https://github.com/trulyeven/trulyeven.github.io/assets/113951017/bb100de5-dd6a-4f21-b964-63c8c58bacfd)

한글 인식이 필요하면 추가 언어에서 체크해주어야 한다

![image](https://github.com/trulyeven/trulyeven.github.io/assets/113951017/4a27b20f-4442-445a-b20e-fc3122c76bf3)
_기본 설치 위치_

아래 환경 변수 설정을 위해 설치 경로를 알아두어야 한다

## 환경 변수 설정

TESSDATA_PREFIX 추가
> C:\Program Files\Tesseract-OCR\tessdata\

path에 추가
> C:\Program Files\Tesseract-OCR\


# Spring Project 세팅

자바에서는 Tesseract를 사용하기 위해서는 추가 의존성이 필요하다
바로 tess4j 이다
이걸 추가해 주면 자바에서도 사용할 수 있게 된다

의존성 추가를 위해 Dependency 설정
```
// gradle - build.gradle
implementation'net.sourceforge.tess4j:tess4j:5.7.0'

// maven
<dependency>
    <groupId>net.sourceforge.tess4j</groupId>
    <artifactId>tess4j</artifactId>
    <version>5.7.0</version>
</dependency>
```


# 간단한 예제

## sample 이미지
![example](https://github.com/trulyeven/trulyeven.github.io/assets/113951017/546b1aff-8833-48dd-b7d7-d3b47e83d73f)
_example.com_


## spring 코드


```java
package com.trulyeven.wocr.controller;

import java.io.File;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;

import net.sourceforge.tess4j.*;

@Controller
public class TransController {

	@GetMapping("trans")
	public String trans() {
		
		File imageFile = new File("C:/Users/example.png");  // 이미지 파일 경로
		ITesseract instance = new Tesseract();
        instance.setDatapath("C:/Program Files/Tesseract-OCR/tessdata"); // tessdata directory 경로

        try {
            String result = instance.doOCR(imageFile);
            System.out.println(result);
        } catch (TesseractException e) {
            System.err.println(e.getMessage());
        }
        
		return "trans";
	}
}
```

## 실행 결과
![image](https://github.com/trulyeven/trulyeven.github.io/assets/113951017/57a9a227-c99a-4315-8f19-ff5474f2e0d6)
_d를 못생기게 써서 ol로 인식됨_

---

참고

[tesseract github 페이지](https://github.com/tesseract-ocr/tessdoc#tesseract-user-manual)
[tess4j.sourceforge.net](https://tess4j.sourceforge.net/)
