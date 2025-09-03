---
title: 왜 로고 이미지를 ::before 에 설정하는가?
date: 2025-08-22 23:58:00 +0900
tags: [css]
categories: [css]
---

# 왜 로고 이미지를 ::before 에 설정하는가?

분명 로고 이미지인데 <img> 태그가 없고, ::before 안에 background 로 base64 문자열의 이미지가 있었다! 
왜인지 궁금해서 ChatGPT에 검색하고 확인한 결과를 기록한다.

```html
<a href="/" class="HeaderView_logo__esVJ4">
  ::before
	<span class="blind">weverse</span>
</a>
```

```css
.HeaderView_logo__esVJ4:before {
    background: no-repeat url(data:image/png;base64,...) 0 0 / contain;
    content: "";
    display: block;
    height: 20px;
    width: 136px;
}
```

`<a>` 안에는 `span.blind` 텍스트만 있고, 실제 눈에 보이는 로고 이미지는 보이지 않는데,
**이미지를 HTML에 직접 `<img>`로 넣지 않고, CSS의 `::before` 가상 요소를 이용해 출력**하기 때문이다.

## 왜 `::before` 에 이미지를 넣을까?

1. **시맨틱 접근성**
   - `<span class="blind">weverse</span>` 는 화면에는 안 보이지만 스크린리더(시각장애인용 보조기기)에서는 읽히게 해서 접근성을 보장.
   - 시각적으로는 로고 이미지, 기술적으로는 텍스트 → SEO/접근성 점수 ↑.
2. **디자인/스타일링 통제**
   - CSS로 로고 교체가 가능 → 다크 모드/이벤트 테마 등 상황에 맞게 로고를 쉽게 바꿀 수 있음.
   - 고해상도 대응(`@2x`, `svg`)도 CSS background-image로 분기 처리하기 편리.
3. **HTML 간결화**
   - 로고 이미지를 HTML `<img>` 로 넣으면 DOM에 리소스 태그가 박히지만, `::before`는 CSS에서 관리 → 마크업은 최소화.
4. **반응형 레이아웃 유연성**
   - 크기/위치 조정, 교체, 숨김 등을 CSS로만 제어 가능 → JS/HTML 수정 없이 스타일시트 레벨에서 대응.

## 요약

**이미지를 `::before`에 넣는 이유는 접근성(시맨틱 + 스크린리더), 테마 교체, CSS 레벨 제어를 쉽게 하기 위해서**이다.
눈에는 이미지, 기계에게는 텍스트 → 사용자 경험과 SEO를 동시에 잡는 패턴이다.