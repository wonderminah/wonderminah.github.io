---
title: CSS 클래스 네이빙 방법론 - BEM (Block, Element, Modifier)
date: 2025-08-23 02:38:00 +0900
tags: [css]
categories: [css]
---



# CSS 클래스 네이빙 방법론 - BEM (Block, Element, Modifier)

CSS 클래스를 작성하다보니 어떤 룰로 적는 것이 Best Practice 인지 궁금해져서 검색해 보다가 BEM에 대해 알게 되었다.
BEM 에 대해서 확인한 내용을 기록한다.

## BEM이란?

BEM CSS는 "Block, Element, Modifier"의 약자로, 웹 개발에서 사용되는 CSS 방법론이다.
CSS 클래스 이름의 명명 규칙을 통해 코드의 구조화, 가독성, 유지보수성, 재사용성을 높이는 것을 목표로 한다.
BEM은 독립적인 컴포넌트(Block)를 구성하는 하위 요소(Element)와, 해당 컴포넌트의 상태나 모양을 나타내는(Modifier) 방식으로 클래스 이름을 작성한다.

## BEM의 각 요소

- **Block (블록):**

  페이지의 독립적이고 재사용 가능한 큰 단위를 의미합니다. 예를 들어, 헤더, 버튼, 카드 등이 블록이 될 수 있습니다. 

- **Element (엘리먼트):**

  블록의 일부로서 독립적인 의미 없이 블록에 종속되는 하위 구성 요소를 의미합니다. 블록의 일부인 로고, 제목, 본문 등이 해당됩니다. 

- **Modifier (모디파이어):**

  블록이나 엘리먼트의 상태나 모양을 변경하는 선택적인 요소입니다. 예를 들어, 버튼의 활성 또는 비활성 상태(`button--active`)나 버튼의 크기(`button--large`) 등을 나타낼 수 있습니다. 

## BEM 클래스 이름의 구성 규칙

- **Block:** 

  `block-name` 형식으로 작성합니다. 

- **Element:** 

  `block-name__element-name`과 같이 두 개의 밑줄(`__`)로 블록과 엘리먼트를 연결합니다. 

- **Modifier:** 

  `block-name--modifier-name` 또는 `block-name__element-name--modifier-name`과 같이 두 개의 대시(`--`)로 블록 또는 엘리먼트와 모디파이어를 연결합니다. 

## 예시 

- **Block:** `.card`
- **Element:** `.card__title`
- **Modifier:** `.card--featured` (카드에 특별한 스타일을 적용)

```css
header__navigation--navi-text
tab__item--focused
```

## BEM을 사용하는 이유

- **가독성 향상:**

  명확한 명명 규칙으로 코드의 의미를 쉽게 파악할 수 있습니다. 

- **유지보수 용이:**

  코드의 구조화로 인해 오류를 찾고 수정하기가 쉬워집니다. 

- **재사용성 증가:**

  독립적인 컴포넌트 단위로 코드를 개발하여 다양한 프로젝트에서 재사용할 수 있습니다. 

- **모듈식 접근:**

  복잡한 웹 페이지를 작은 단위로 분리하여 개발 효율성을 높입니다. 

## 참고

https://bem-cheat-sheet.9elements.com/

