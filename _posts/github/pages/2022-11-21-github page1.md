---
title : "github page 블로그 만들기(jekyll)-1"
date : 2022-11-22 12:00:01 +0900 # +/-TTTT
categories : [github, pages]
tags : [github, github pages, jekyll] #소문자만 가능
---




## Github에서 주소 생성하기

---

- github에서 새 repository 생성

![Desktop View](/assets/img/github/create.png){: width="500" height="400" }
_Repository name = [username].github.io_

[username].github.io로 생성하면 자동으로 github pages로 생성된다.

> `git`을 통한 과정은 이 포스트에서는 생략한다.
{: .prompt-warning }

---
<br>



## Ruby, Jekyll 설치하기

---

루비 설치하기<br>
<https://rubyinstaller.org/downloads/>

DEVKIT이 있는 버전을 다운한다.
> Jekyll이 32bit이기 때문에 64bit로 설치하면 터미널에서 인식하지 못하고 설치된 `Command Prompt with Ruby`에서 작업해야 한다.
{: .prompt-tip }

- Ruby 설치

![Desktop View](/assets/img/github/rubyinstall.png){: width="500" height="400" }
_MSYS2 development toolchain 항목을 체크해준다_

- Ruby 설치완료 후 실행 화면

![Desktop View](/assets/img/github/ruby.png){: width="500" height="400" }
_1,3번 또는 그냥 Enter 입력 설치완료 되면 한번 더 Enter_

<br>

#### Console 또는 Ruby 콘솔에서 jekyll bundler 설치

```bash 
# jekyll 설치 확인
jekyll -v
# jekyll 버전이 출력되면 정상 설치 완료

# jekyll bundler 설치
gem install jekyll bundler  
```

---
<br>



## jekyll로 사이트 생성

---

github와 연결된 레포지드 폴더 위치설정 후
```bash 
jekyll new ./
bundle install

# 로컬 서버 실행
bundle exec jekyll serve --trace
```
<http://127.0.0.1:4000/> 로컬 서버 주소


![Desktop View](/assets/img/github/jekyllfirst.png){: width="500" height="400" }
_접속 시 화면_

<br>

접속에 성공했으면 `github`에 `push`하면 사이트 작성 완료

---
