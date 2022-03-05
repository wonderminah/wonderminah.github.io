---
title: "jekyll 블로그에 Google Analytics 도입"
date: 2022-02-07 08:49:00 +0900
toc: true
toc_icon: bars
toc_sticky: true
comments: true
author_profile: false
tags: [jekyll, google-analytics]
---

# Google Analytics 계정 만들기

계정 및 앱 생성 과정은 생략.    
생성을 완료하고 나면 다음과 같이 태그 이용에 대한 화면을 확인할 수 있다.

![image-20220207083258339](https://wonderminah.github.io/assets/img/image-20220207083258339.png)

추적용 태그 삽입에는 [Google 태그 관리자와 gtag.js](https://support.google.com/tagmanager/answer/7582054) 두 가지 방식이 있는 것 같은데, 우선은 별도의 작업 없이 빨리 설치하고 싶었기에 gtag.js를 이용하기로 했다. 역시나 언제든지 전환할 수 있다는 아래 문구를 확인한 후 말이다.

> gtag.js를 이미 사용 중이라면 나중에 언제든지 태그 관리자로 업그레이드할 수 있습니다.

# gtag.js를 jekyll 블로그에 삽입

_config.yml에 다음과 같이 analytics 정보를 입력한다.

```yml
analytics:
  provider               : google-gtag
  google:
    tracking_id          : 추적하고자 하는 앱의 트래킹 ID (애널리틱스 관리자 페이지에서 확인 가능)
    anonymize_ip         : # true, false (default)
```

_includes 아래의 [analytics.html](https://github.com/mmistakes/minimal-mistakes/blob/master/_includes/analytics.html) 및 [analytics-providers/google-gtag.html](https://github.com/mmistakes/minimal-mistakes/blob/master/_includes/analytics-providers/google-gtag.html)를 minimal-mistakes로부터 그대로 가져온다.

```bash
├── _config.yml
├── _includes
│   ├── analytics.html
│   └── analytics-providers
│       └── google-gtag.html
└── run.sh
```

# 결과

페이지 접속 시 gtag.js가 접속 내용을 구글로 전송한다.

![image-20220207084635927](https://wonderminah.github.io/assets/img/image-20220207084635927.png)

추적된 내용을 애널리틱스 보고서에서 확인 가능하다.

![image-20220207084317223](https://wonderminah.github.io/assets/img/image-20220207084317223.png)

