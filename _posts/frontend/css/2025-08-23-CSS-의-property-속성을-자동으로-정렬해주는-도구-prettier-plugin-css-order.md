---
title: CSS 의 property 속성을 자동으로 정렬해주는 도구, prettier-plugin-css-order
date: 2025-08-23 02:38:00 +0900
tags: [css, prettier-plugin-css-order]
categories: [css]
---

# CSS 의 property 속성을 자동으로 정렬해주는 도구, prettier-plugin-css-order

CSS 의 property 속성을 알파벳 순으로 정렬하는 것이 Best Practice 인가? 하고 의문이 들어 검색하다 보니, 꼭 그렇지는 않다는 답변과 함께, property 속성을 일관된 순서로 정렬해주는 prettier-plugin-css-order 라는 것을 알았다. 사용 방법에 대해 정리한다.

## 패키지 설치

프로젝트의 패키지 관리자를 통해 `prettier-plugin-css-order` 플러그인을 설치한다.

```bash
npm install postcss prettier-plugin-css-order --save-dev
```

## **Prettier 설정**

프로젝트 루트에 `prettier.config.cjs`  을 만들고 아래와 같이 작성한다.

```js
module.exports = {
  plugins: ["prettier-plugin-css-order"],
  cssDeclarationSorterOrder: "smacss",
};
```

### 파일 확장자가 `.js` 가 아니라 `.cjs`인 이유?

.js 로 설정했을 때는, 아래와 같은 에러가 발생했다.

```bash
➜  weverse-clone-coding git:(main) ✗ vi prettier.config.js
➜  weverse-clone-coding git:(main) ✗ npx prettier --write "src/**/*.{js,jsx,ts,tsx,css,scss}"

[error] Invalid configuration for file "/Users/minah.kim/Projects/weverse-clone-coding/src/App.tsx":
[error] module is not defined in ES module scope
[error] This file is being treated as an ES module because it has a '.js' file extension and '/Users/minah.kim/Projects/weverse-clone-coding/package.json' contains "type": "module". To treat it as a CommonJS script, rename it to use the '.cjs' file extension.
```

`package.json` 안에 `"type": "module"` 이 있어서, `prettier.config.js` 가 **ESM(ECMAScript Module)** 으로 취급되고 있는데,  `prettier.config.js` 안에서 `module.exports = { ... }` (CommonJS 문법)을 쓰니까 충돌이 난 것이다. `.cjs`로 할 경우 Prettier 가 CommonJS 로 읽어주기에 문제가 해결된다.

### cssDeclarationSorterOrder 종류

아래 3가지가 있다.

1) `alphabetical`: 속성을 알파벳순으로 정렬
2) `smacss`: SMACSS 방식 (많이 쓰임)
   1) Positioning (position, top, right, bottom, left, z-index …)
   2) Box model (display, float, width, height, margin, padding, border …)
   3) Typographic (font, text-align, line-height, color …)
   4) Visual (background, box-shadow, opacity, transform …)
   5) Miscellaneous (cursor, pointer-events, etc.)
3) `concentric-css`: 안쪽에서 바깥쪽으로 concentric(동심원) 순서
   - margin/padding → border → background → text → 기타 식으로 “상자 모델을 안에서 밖으로” 정렬

## 정렬 실행

```bash
➜  weverse-clone-coding git:(main) ✗ npx prettier --write "src/**/*.{js,jsx,ts,tsx,css,scss}"

src/App.tsx 44ms (unchanged)
src/index.css 15ms (unchanged)
src/main.tsx 4ms (unchanged)
src/vite-env.d.ts 1ms (unchanged)
```

이렇게 정렬을 해준다!