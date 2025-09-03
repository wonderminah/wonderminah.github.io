---
title: CSS 영역 구분을 위한 선택자로써 class 를 써야하나, id 를 써야하나?
date: 2025-09-03 22:40:00 +0900
tags: [css]
categories: [css]
---



# CSS 영역 구분을 위한 선택자로써 class 를 써야하나, id 를 써야하나?

고유한 CSS 영역 구분을 위해 id 로 작성을 하였는데, 내가 클론코딩을 위해 참고했던 Spotify 나 Weverse 는 대부분 class 를 쓰고 있었기에 무엇이 Best Practice 인지 궁금해졌다.

```html
{/* 헤더 */}
      <div id="header__area">
        <header id="header__wrap">
          <div id="header__service">
            <h1 id="header__logo-wrap">
              <a id="header__logo-link" href="/" >
                <span id="header__logo">weverse</span>
              </a>
            </h1>
          </div>
        </header>
      </div>
```

## 문제점

1. **id는 고유해야 함**
   - 한 페이지에 같은 `id`가 두 번 있으면 HTML 표준 위반.
   - 지금 네이밍은 "고유"라기보다는 그냥 **구조적 class 이름처럼 보임**.
2. **스타일 재사용 불가능**
   - id는 한 요소에만 적용돼.
   - 만약 비슷한 `header__logo` 스타일을 다른 페이지에서도 쓰고 싶으면 `id` 때문에 재사용이 안 돼.
3. **CSS 우선순위 꼬임**
   - id는 specificity(우선순위)가 너무 강해서, 나중에 class로 override하기 힘들어져.
   - 유지보수하다 보면 `!important` 남발하게 될 가능성이 큼.

다른 것은 몰라도 3. 은 조금 신경이 쓰인다.

## 더 권장되는 방식: class로 변환

```html
{/* 헤더 */}
<div class="header__area">
  <header class="header__wrap">
    <div class="header__service">
      <h1 class="header__logo-wrap">
        <a class="header__logo-link" href="/" >
          <span class="header__logo">weverse</span>
        </a>
      </h1>
    </div>
  </header>
</div>
```

## 스타일 예시

```css
.header__area {
  background: #fff;
}

.header__logo {
  font-size: 24px;
  font-weight: bold;
}
```

## 정리

- 지금 네가 작성한 건 **id 네이밍은 BEM 같지만, 용도는 class에 맞는 것**이야.
- 따라서 **id → class로 바꾸는 게 베스트**.
- id는 나중에 진짜 **한 요소만 딱 집어야 할 때 (예: `#app-root`, `#modal`)** 남겨둬.

## 결론

class 로 바꿨다.