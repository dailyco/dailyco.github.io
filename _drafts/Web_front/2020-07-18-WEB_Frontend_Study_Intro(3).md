---
layout: post
title: "WEB Front-end 공부 일기 : HTML, CSS, JS 개요 (3)"
date: 2020-07-18
categories: Front-end
tags: web front study html css js
sitemap:
    changefreq: daily
---

본 포스팅은 CSS에 관련한 내용으로 기본적인 CSS 형태, 선택자와 속성의 종류, CSS를 선언하는 세 가지 방식에 대해 이야기한다. 매우 기본적인 이야기이기도 하고 추 후에 CSS를 자세히 다루기 때문에 굳이 정리할 필요는 없지만, HTML과 마찬가지로 살짝 맛보기만 해보려 한다.  
<br/>

<br/>

### 💡알림💡
본 일기는 패스트 캠프의 '프론트엔드 개발 올인원 패키지 with React Online' 강의를 기반으로 공부한 내용을 복습할 목적으로 작성함을 밝히며, 잘못된 부분이 존재할 수도 있음을 알립니다! 잘못된 부분은 댓글로 말씀해주시면 감사하겠습니다 ʕ•̀ω•́ʔ✧
<br/><br/>

### ⏰ㅤWEB Front-end 공부 일기 1
첫 날 공부한 내용은 HTML과 CSS의 개요이다. HTML, CSS, JS가 뭔지 그리고 아주 기본적인 내용들에 대해 공부했다.
<br/><br/><br/>
    
## 1. 기본 형태
```css
선택자 {
	속성: 값;
	속성: 값;
	...
}
```
- 선택자(Selector): HTML에 스타일을 적용할 때 적용하고자 하는 HTML 특정 요소(태그)를 선택하는 sign
- 속성(Properties): 스타일을 적용할 내용
- 값(Value): 속성에 해당하는 실제 값
<br/><br/>

### 예시

```css
div {
	font-size: 20px; /* 글자 크기는 20px */
	color: red; /* 글자 색은 빨간색 */
	width: 300px; /* 가로 너비는 300px */
	margin: 20px; /* 바깥 여백은 20px */
	padding: 10px 20px; /* 안쪽 여백 위아래 10px, 좌우 20px */
	position: absolute; /* 위치는 부모요소 기준 */
}
```
<br/><br/><br/><br/>

## 2. 선택자 종류
### 태그로 찾기
```css
태그 이름 {
	속성: 값;
}
```
<br/>

### 클래스로 찾기
```css
/* CSS */
.클래스이름 {    /* .은 클래스 선택자 */
	속성: 값;
}

/* HTML */
<TAG class="클래스이름">CONTENTS</TAG>
```
<br/><br/><br/><br/>

## 3. 속성 종류 (기본)
- 속성의 기본값은 16px
- width (가로 너비) / 단위: px
- height (세로 너비) / 단위: px
- font-size (글자 크기) / 단위: px
- 단축 속성: margin (요소 바깥 여백)  
개별 속성: margin-top, margin-right, margin-bottom, margin-left
- 단축 속성: padding (요소 내부 여백)  
개별 속성: padding-top, padding-right, padding-bottom, padding-left
- color (글자 색상)
- 단축 속성: background (요소 배경 색상 + @)  
개별 속성: background-color (요소 배경 색상) + @
<br/><br/><br/><br/>

## 4. CSS 선언방식 3가지
### 1. 인라인 선언 형식

```html
<div style="color: red;">CONTENTS</div>
```
- 선택자가 필요없다
- 적용해야할 동일한 태그가 많을 때, 수정시 비효율적
<br/><br/>

### 2. HTML 내장 형식

```html
<head>
  <style>
    div {
      color: red;
    }
  </style>  
</head>
<body>
  <div>HTML에 포함1</div> <!-- 색상: 빨강 -->
  <div>HTML에 포함2</div> <!-- 색상: 빨강 -->
</body>
```
<br/>

### 3. 외부에서 불러오는 형식

```css
/* ./css/main.css */
div {
	color: red;
}
```
<br/>

```html
<head>
  <link rel="stylesheet" href="./css/main.css">
</head>
<body>
  <div>HTML에 외부에서 불러오기1</div> <!-- red -->
</body>
```
- 한 번 선언해 둔 것을 여러 HTML에 적용 가능

<br/><br/><br/><br/>

## 5. Refernece
- [HEROPY Tech - 입문자에게 추천하는 HTML, CSS 첫걸음](https://heropy.blog/2019/04/24/html-css-starter/)
<br/><br/><br/><br/>