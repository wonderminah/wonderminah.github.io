---
title: Jekyll 블로그를 Google Search Console에 등록하는 방법
date: 2025-04-02 23:00:00 +0900
tags: [jekyll, google-search-console]
---

# 1. Google Search Console 에 URL 등록

URL prefix 에 `https://wonderminah.github.io/` 를 입력하고 CONTINUE를 클릭한다.

![image-20250402223835540](../assets/img/image-20250402223835540.png)

이미 예전에 HTML 파일 등록을 완료해 두었기 때문에 auto verified 라고 뜬다. HTML 파일 등록은 바로 밑에 후술한다.

![image-20250402223842255](../assets/img/image-20250402223842255.png)

# 2. HTML 파일 등록

좌측 네비게이션에서, 등록된 `https://wonderminah.github.io/` 를 클릭한다.

![image-20250402223857867](../assets/img/image-20250402223857867.png)

Ownership verification을 클릭한다. (이미 인증이 완료된 상태라 초록색 마크가 표시되지만, 미인증 상태에서는 다르다.)

![image-20250402224223593](../assets/img/image-20250402224223593.png)

클릭하면 HTML 파일을 다운로드 하는 화면이 표시된다. HTML 파일을 아래와 같이 프로젝트 루트에 두고 push한다.

![image-20250402224334349](../assets/img/image-20250402224334349.png)

참고로 HTML 내용은 아래와 같다.

```html
google-site-verification: google6c476340d19371a9.html
```

몇 분 지나 새로고침을 하면, 위의 스크린샷과 같이 소유권 인증이 완료되었다는 초록색 마크가 표시될 것이다.

# 3. sitemap.xml 생성 및 등록

jekyll 은 프로젝트 루트의 _config.yml 에 `jekyll-sitemap` 플러그인을 활성화할 경우, 자동으로 sitemap.xml 를 생성해준다.

```xml
# Plugins (previously gems:)
plugins:
  - jekyll-paginate
  - jekyll-sitemap
```

https://wonderminah.github.io/sitemap.xml 에 접속하면 sitemap.xml 이 자동으로 최신 버전으로 생성되어 있는 것을 알 수 있다.



하지만 Google Search Console 에서 sitemap.xml 의 Status 를 확인해 보니, Couldn't fetch 상태였다.

![image-20250402225440896](../assets/img/image-20250402225440896.png)

sitemap.xml 을 입력하고 다시 한 번 SUBMIT 해주었다.

![image-20250402225536957](../assets/img/image-20250402225536957.png)

sitemap.xml 의 Submitted 가 Apr 2, 2025 로 갱신되었다. Status 는 조금 더 기다려보자.

![image-20250402225555425](../assets/img/image-20250402225555425.png)

# 4. robots.txt 생성

웹 크롤러들에게 크롤링 규약을 알려주기 위한 파일이다.
아래와 같은 파일을 만들고, 프로젝트 루트에 위치시켜 준다.

```
User-agent: *
Allow: /
Sitemap: https://wonderminah.github.io/sitemap.xml
```

`User-agent: *` 모든 User-agent 를 허용
`Allow: /` 웹 사이트 내의 모든 path에 대한 크롤링을 허용
`Sitemap:` sitemap.xml 의 URL를 기재

# 5. 구글 검색결과 확인

하루~이틀 후 확인해보니, 다음과 같이 검색결과에 나타나게 된 걸 확인할 수 있었다.

![image-20250404012402563](../assets/img/image-20250404012402563.png)