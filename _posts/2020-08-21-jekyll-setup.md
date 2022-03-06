---
title: "jekyll 블로그 초기구축 로그"
date: 2020-08-21 01:12:00 +0900
tags: [jekyll]
---

# 최소한의 구축 과정

## 새로운 repository 작성

자신의 username 뒤에 `github.io`가 붙은 이름으로 작성한다.

![image-20200821003558829](../assets/img/image-20200821003558829.png)

## theme 적용

잘 알려져 있는 jekyll을 이용하기로 했다.
수많은 테마 중 가장 많은 유저들이 사용하는 minimal-mistakes라는 테마를 적용해보기로 했다.
[jekyll 테마 목록](https://github.com/topics/jekyll-theme)

### _config.yml 파일 가져오기

여기서는 minimal-mistakes의 [_config.yaml](https://github.com/mmistakes/minimal-mistakes/blob/master/_config.yml) 파일의 내용을 일부 수정하고 내 repository에 commit을 할 것이다.
먼저 파일을 열어, 아래 부분의 주석을 해제한다.

```bash
# remote_theme           : "mmistakes/minimal-mistakes"
```

url에 미리 생성한 repository의 hostname을 입력한다.
(url: the base hostname & protocol for your site e.g. "https://mmistakes.github.io")

```bash
url                      : "https://wonderminah.github.io"
baseurl                  : # the subpath of your site, e.g. "/blog"
```

그 외, title, name, description을 원하는 내용으로 수정한다.

```bash
title                    : "Wonderminah Tech Blog"
name                     : "Wonderminah Tech Blog"
description              : "Wonderminah Tech Blog"
```

repository에 push한다.
위치는 최상단. (wonderminah.github.io/_config.yaml)

### index.html 파일 가져오기

[index.html](https://github.com/mmistakes/minimal-mistakes/blob/master/index.html)의 파일을 그대로 가져와 repository에 push한다.
역시 위치는 최상단. (wonderminah.github.io/index.html)

## 동작 확인

브라우저에서 https://wonderminah.github.io에 접속.
블로그가 표시되는 것이 확인 가능하다.

# 사용 방법

## 새 post를 작성하고 싶을 시

repository 최상단에 _posts라는 이름의 디렉토리 생성.
마크다운 파일을 작성

```bash
---
title: "ESLint의 개념 및 사용 예시"
date: 2020-08-19 23:09:00 -0400
categories: react-native
---
# 여기서부터 마크다운으로 포스트를 작성한다.
```

규칙에 맞게 네이밍 (예: 2020-08-19-ESLint의 개념 및 사용 예시.md) 후 push.
매핑되는 url `wonderminah.github.io/{category 이름}/{작성한 md파일에서 날짜를 제외한 부분}/`을 따르게 되며, 아래에서 확인할 수 있다.
[https://wonderminah.github.io/react-native/ESLint%EC%9D%98-%EA%B0%9C%EB%85%90-%EB%B0%8F-%EC%82%AC%EC%9A%A9-%EC%98%88%EC%8B%9C/](https://wonderminah.github.io/react-native/ESLint의-개념-및-사용-예시/)

## 글에 이미지를 삽입하고 싶을 시

더 좋은 방법이 있는지는 모르겠으나, 나는 맥북에서 스크린샷 후 로컬에 자동으로 저장된 이미지를 repository로 옮겨 push한 후, 그에 매핑되는 블로그 url을 마크다운 문서에 작성하는 방식을 사용하고 있다.

repository 최상단에 assets/img 디렉토리 작성하고 그 안에 이미지 파일을 저장한다.
react-native 카테고리의 포스트에서 삽입했던 이미지의 로컬 파일 패스와 마크다운 작성 시 문법은 각각 아래와 같다.

```bash
# 로컬 파일 패스
/Users/minah.kim/Desktop/development/wonderminah.github.io/assets/img/image-20200819233603148.png
# 마크다운 작성 시 문법
![image-20200821003558829](../assets/img/image-20200819233603148.png
```

개인적으로는 조금 귀찮은 방법이다.
차후 다른 좋은 방법을 사용하게 될 경우 추가 기록 예정.