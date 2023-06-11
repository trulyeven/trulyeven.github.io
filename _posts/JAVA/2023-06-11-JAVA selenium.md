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

---

# 2. selenium

웹 크롤링(crawling), 웹 스크랩핑(Scraping)을 하는 데 사용되는 라이브러리

- 빅데이터관련, 동적인 자료를 수집할 때 주로 사용한다
- 브라우저 드라이버를 사용하여 동적 데이터도 수집 가능하다
- Jsoup에 비해 속도는 느리다 

Jsoup
: HTTP Request를 사용하여 정적으로 자료를 수집하는 라이브러리

[selenium 다운로드 페이지](https://www.selenium.dev/downloads/)

---

# 3. Web Driver

여기서는 Microsoft Edge 브라우저를 사용하여 selenium을 실행한다
다른 브라우저의 경우 알맞는 브라우저 드라이버를 설치하면 된다

먼저 자신의 브라우저의 버전을 확인한다
![image](https://github.com/trulyeven/vocr/assets/113951017/7f0e9d6d-9509-43af-ac05-386b07dbe2f3)

[Edge driver 다운로드 사이트](https://developer.microsoft.com/ko-kr/microsoft-edge/tools/webdriver/)

그리고 버전에 맞는 웹 드라이버를 다운로드해서 적절한 폴더에 옮겨준다

> edge가 최신 버젼이라 맞는 버전이 없는 경우 가장 가까운 버전을 다운 받아준다<br>
  그러면 경고가 뜨긴 하지만 실행 시 알아서 가까운 버전에 맞추어 실행된다<br>
  혹시나 오류가 나는 경우 브라우저의 버전을 다운그레이드 해주어야 한다<br>
{: .prompt-info }

---

# 4. spring에서 실행

## 4.1 denpendency

```java
// build.gradle
implementation'org.seleniumhq.selenium:selenium-java:4.9.1'

// pom.xml
<dependency>
    <groupId>org.seleniumhq.selenium</groupId>
    <artifactId>selenium-java</artifactId>
    <version>4.9.1</version>
</dependency>

```

## 4.2 간단한 예제 code
```java
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.edge.EdgeChromeDriver;

public void open() {
    System.getProperty("webdriver.edge.driver", "C:\\worktool\\msedgedriver.exe");  // 웹드라이버 위치
    WebDriver driver = new EdgeDriver();
    driver.get("https://www.naver.com");  // 제어할 사이트 열기
                    
    driver.quit();  // 종료
}
```

> `http://`, `https://`를 적지 않으면 'data:,' 주소를 가진 빈사이트가 열릴 수 있음


참고  
[selenium 공식 documentation](https://www.selenium.dev/documentation/)

