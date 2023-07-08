---
title : "github page 블로그 만들기(jekyll)-2"
date : 2022-11-23 16:03:11 +0900 # +/-TTTT
categories : [github, pages]
tags : [github, github pages, jekyll, chripy] #소문자만 가능
---


## jekyll 테마

---
`github pages`가 `jekyll`을 사용하면 간단하게 테마을 입힐 수 있다.

<http://jekyllthemes.org/>

위의 사이트뿐만 아니라 여러 무료 테마를 제공하는 사이트가 많다.
여기서 깔끔하고 기본기능이 충실한 chripy 테마를 선택해 적용하겠다.

<https://github.com/cotes2020/jekyll-theme-chirpy>

`<>code` 버튼을 눌러 `zip` 파일을 다운 후 압축을 풀고

`githup pages`에 적용된 로컬 폴더에 덮어쓴다

---
<br>


## 테마 적용하기

---

테마가 개발자에 맞게 수정되어 있어서 초기화 후에 사용해야 한다. 

chirpy 테마 `_posts` 폴더의 `getting-started`에 설명이 나와있다.

```
bash tools/init.sh
```

이 명령어를 실행하면 초기화가 간단히 되지만 `bash`가 리눅스 명령어기 때문에 사용할 수 없었다.

그래서 수동으로 파일을 수정해 준다.


### 삭제 및 수정

> 수정 2023-07-09 현재 chirpy theme 최신버전을 사용할 경우 이 과정을 생략해도 된다.
{: .prompt-warning }

- 삭제 할 폴더 및 파일
  + `.travis.yml`
  + `_posts` 하위 파일
  + `docs` 폴더
- `.gitignore` 파일
  + `Gemfile.lock` 구문 지우기
- .github/workflows/ 경로에서
  + `pages-deploy.yml.hook` 제외한 나머지 파일 삭제
  + `pages-deploy.yml.hook` ➡ `pages-deploy.yml` 이름 변경

---
<br>


## _config.yml 수정

---
 - 메모장이나 코드편집기를 사용해서 수정해준다.

    * timezone: Asia/Seoul
    * title: 블로그 제목
    * tagline: 태그라인
    * description: 블로그 설명
    * url: ‘https://[username].github.io’
    * github: username: github_username
    * twitter: username: twitter_username
    * google_analytics: 구글 애널리틱스 연결
    * google_analytics: pv: 구글 애널리틱스 GA 연결
    * avatar: 프로필 사진 넣기
    * img_cdn: 이미지 불러오는 기본 주소로 주석처리 하거나 삭제해야 로컬로 불러올 수 있다
    * img_cdn 수정 시 avatar 위치를 수정해주지 않으면 오류 발생! assets/img/[원하는 아바타 파일명]


![Desktop View](/assets/img/github/localtest.png){: width="auto" height="auto" }
_로컬 서버 접속 시 화면_

# bundle 설치, 로컬 서버 실행
``` 
cd [clone된 local repo 경로]

bundle install

bundle exec jekyll serve
```
<http://127.0.0.1:4000/>
로컬로 사이트가 바뀐 것을 확인할 수 있다.

![Desktop View](/assets/img/github/localtest.png){: width="auto" height="auto" }
_로컬 서버 접속 시 화면_

PUSH를 하면 이제 url에서 작성한 사이트에서도 적용이 된다.

---





## 에러 발생?

---

> --- layout: home # Index page ---

사이트 접속 시 테마가 적용된 사이트가 나오지 않고 위의 글이 나오는 경우가 있다.

이 경우에 문제가 나타난 이유는 Linux 기반 컴퓨터가 배포를 처리하는 동안 Windows에서 사이트를 번들로 묶었기 때문이라는 추측된다.

PUSH 하기 전에 아래의 명령어를 입력해주면 된다.

#### Console창, 64bit는 Ruby Console창에서

```bash
bundle lock --add-platform x86_64-linux
```

이 후 PUSH하면 정상적으로 사이트가 표시된다

---
<br>

