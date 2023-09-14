---
title : "[github] github actions 배포 에러 (ERROR: Invalid first code point of tag name U+BC30.)"
date : 2023-09-13 00:00:00 +0900 # +/-TTTT
categories : [github]
tags : [github, actions, error] #소문자만 가능
math : true
# mermaid : false
image:                         # 미리보기 이미지
  path: https://github.com/trulyeven/trulyeven.github.io/assets/113951017/95de9e69-d9d8-44c7-9426-0502de27a921
  width: 700                  # in pixels
  height: 400                  # in pixels
  alt: github actions
---

```
HTML-Proofer found 2 failures!

Error: Process completed with exit code 1.
```

이 블로그는 jekyll-theme-chirpy 테마를 사용하고 있다

github actions를 통해서 자동으로 빌드하고 배포해주는 방식을 사용하고 있다

새로운 포스트를 작성 중 위와 같은 에러가 발생했다

`htmlproofer`에서 이상한 문법을 감지하고 에러를 보낸 것이다


```
1:12400: ERROR: Invalid first code point of tag name U+BC30.
```

태그 네임 오류, kotlin 포스트 작성 중 자료형 `< >` 가 문제였다

```
arrayOf<배열 값의 타입>(값, ...)

                ↓

arrayOf\<배열 값의 타입\>(값, ...)
```

`< >` 앞에 각각 `\`를 추가해주니 해결되었다