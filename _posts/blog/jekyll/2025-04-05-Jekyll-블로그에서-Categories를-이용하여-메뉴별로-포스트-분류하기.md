---
title: Jekyll 블로그에서 categories-archive 플러그인을 이용하여 메뉴별로 포스트 분류하기
date: 2025-04-04 02:28:00 +0900
tags: [jekyll]
categories: [jekyll]
---

글을 몇 개 쓰다보니 카테고리별로 분류를 하고싶어 좌측 네비게이션 메뉴를 정리하였다.
그런데, 이 메뉴를 클릭했을 때 표시되는 화면에 어떻게 글을 모을 수 있는지 알아보니, categories-archive 플러그인으로 가능했다.
다만, 기본적으로는 다중 계층 카테고리를 지원하지 않는 듯 했다. (그럼 categories 말고 category 라고 단수형을 써주던가...)
우선은 단일 계층 카테고리로 구현하였고 그에 대한 내용을 정리한다.

# 1. 각 포스트 .md 파일의 yaml에 카테고리 추가

포스트 마크다운 파일 안의 YAML 프론트매터에 `categories:` 가 지정이 되어있어야 한다. 이 포스트를 예를 들면 아래와 같다.

```yaml
title: Jekyll 블로그에서 categories-archive 플러그인을 이용하여 메뉴별로 포스트 분류하기
date: 2025-04-05 02:28:00 +0900
tags: [jekyll]
categories: [jekyll] # 이렇게 하면, /jekyll/포스트명 과 같은 URL 이 만들어진다.
# categories: [blog, jekyll] # 이렇게 하면, /blog/jekyll/포스트명 과 같은 URL 이 만들어진다.
# 다만 categories-archive 가 /blog/jekyll/ 링크만을 지원하고, /blog/ 와 같은 상위 URL을 지원하지 않았다.
```

`categories: [blog, jekyll]` 와 같이 Parent 와 Child 메뉴를 모두 지정하고 Parent 별 포스트 모음 페이지도 만들까 싶었지만, 상술했듯이 우선은 단일 계층으로 진행하도록 하자.

# 2. categories-archive 플러그인 활성화

주석처리 되어있던 아래 코드를 주석 해제하여 플러그인을 활성화 하였다.

```yaml
jekyll-archives:
  enabled:
    - categories
    - tags
  layouts:
    category: archive-taxonomy
    tag: archive-taxonomy
  permalinks:
    category: /:categories/ # categories 가 'jekyll'일 경우, /jekyll/ 로 포스팅이 모이게 된다.
    tag: /tags/:name/
```

# 3. 좌측 네비게이션에 path 지정

`_data/navigation.yml` 에서 url을 지정한다.

```yaml
# documentation links
docs:
  - title: Blog
    children:
      - title: "Jekyll Blog"
        url: /jekyll/ # 여기
```

# 4. (없을 경우) archive-taxonomy.html 추가

minimal-mistakes 테마에는 `_layouts/archive-taxonomy.html` 템플릿이 이미 포함돼 있어서 별도 작성이 필요 없다고 하는데, 왜인지 내 디렉토리에는 없었다. [Minimal Mistakes GitHub 리포지토리](https://github.com/mmistakes/minimal-mistakes/blob/master/_layouts/archive-taxonomy.html) 에서 직접 다운로드하여 디렉토리에 추가했다.

# 5. 결과

완료.

![image-20250405021711934](/assets/img/image-20250405024739765.png)