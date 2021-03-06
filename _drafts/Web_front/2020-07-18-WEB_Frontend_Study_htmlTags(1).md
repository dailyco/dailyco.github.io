---
layout: post
title: "WEB Front-end 공부 일기 : HTML 요소 - 콘텐츠 구분 & 문자 콘텐츠"
date: 2020-07-18
categories: Front-end
tags: web front study html
sitemap:
    changefreq: daily
---

역시 내용이 많아서 세 포스팅으로 나누게 되었다. 이번 포스팅에서는 HTML의 태그에 대해서 자세히 하나씩 살펴보는데, 태그 중에서도 콘텐츠를 구분하는데 사용하는 태그들과 문자 콘텐츠를 나타내는 태그들에 대해서 공부한다. 그냥 무작정 무슨 태그인지 배우는 것보다 하나씩 어디에 사용하는건지 공부하니까 훨씬 이해가 잘되고 웹 페이지를 만들때 어떤 태그를 사용하는 것이 옳은 것인지를 배울 수 있어서 좋은 것 같다 (\*´ ˘ `\*)  
<br/>

<br/>

### 💡알림💡
본 일기는 패스트 캠프의 '프론트엔드 개발 올인원 패키지 with React Online' 강의를 기반으로 공부한 내용을 복습할 목적으로 작성함을 밝히며, 잘못된 부분이 존재할 수도 있음을 알립니다! 잘못된 부분은 댓글로 말씀해주시면 감사하겠습니다 ʕ•̀ω•́ʔ✧
<br/><br/>

### ⏰ㅤWEB Front-end 공부 일기 2
먼저는 HTML 태그에는 어떤 종류가 있는지 전체적인 개요를 알아보고, 블록 요소와 인라인 요소들에 대해서 배우면서 무엇이 다른지 그 특성에 대해 알아보았다. 그리고 구체적으로 요소를 하나씩 알아보면서 어디에 쓰는 요소이고 어떤 속성과 특성을 가지는지 공부했다.
<br/><br/><br/>

## 1. 콘텐츠 구분 요소
### <header>  
- 웹사이트 상단에 로고, 메뉴 등이 있은 곳에 사용
- \<header\>는 \<address\>, \<footer\>, 다른 \<header\>의 자식 요소가 될 수 없다
- 속성: 전역 속성
- [MDN: <header>](https://developer.mozilla.org/ko/docs/Web/HTML/Element/header)
<br/><br/>

### <footer>
- header와 반대로 웹사이트 하단에 위치
- 일반적으로 저작권자, 연락처 등의 정보를 담고있다
- \<footer\>는 \<address\>, \<header\>, 다른 \<footer\>의 자식 요소가 될 수 없다
- 속성: 전역 속성
- [MDN: <footer>](https://developer.mozilla.org/ko/docs/Web/HTML/Element/footer)  

✨ 사실 레이아웃을 만들 때 footer 대신 div를 사용해도 되지만, HTML5에서는 semantic tag라고 불리는 의미를 가진 태그들이 존재한다.  
그래서 이를 적재적소에 사용하는 것이 중요하다.
<br/><br/>

### <h1> - <h6>
- \<h1\> - \<h6\> 요소는 6단계의 구획 요소를 나타낸다
- 글씨 크기를 줄이기 위해서는 낮은 단계의 <h>를 사용하지 말고 CSS의 font-size 속성을 사용해야한다
- 중첩의 경우 h1부터 h6로 내려가면서 컨텐츠 구조를 나타내야한다
- 되도록 \<h1\>은 한 번만
- 속성: 전역 속성
- [MDN: <h1> - <h2>](https://developer.mozilla.org/ko/docs/Web/HTML/Element/Heading_Elements)

#### 예시
![h1-h6](https://s3.us-west-2.amazonaws.com/secure.notion-static.com/a4604b2e-7d8f-4a55-b5b1-eba5899908cb/_2020-07-15__6.44.50.png?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Credential=AKIAT73L2G45O3KS52Y5%2F20200718%2Fus-west-2%2Fs3%2Faws4_request&X-Amz-Date=20200718T124733Z&X-Amz-Expires=86400&X-Amz-Signature=972721f9b1d19a051c89a3270ce1b06d50b44f47f8b739b039cef7618fdfb9b4&X-Amz-SignedHeaders=host&response-content-disposition=filename%20%3D%22_2020-07-15__6.44.50.png%22)
<br/><br/>

### <main>
- \<main\>은 문서나 앱의 주요 콘텐츠를 나타낸다
- hidden 속성 없이는 문서에 하나만 존재
- IE 지원 X
- [MDN: <main>](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/main)
<br/><br/>

### <article>
- \<article\>은 '독립적으로'구분되거나 '재사용 가능'한 영역을 설정  
독립적으로 구분된다: 따로 분리 하더라도 해당 컨텐츠 그대로 다른 곳에서 사용 가능한 경우
- 주로 신문 기사나 블로그 글에 쓰인다
- [MDN: <article>](https://developer.mozilla.org/ko/docs/Web/HTML/Element/article)
<br/><br/>

### <section>
- \<section\>은 문서의 일반적인 영역을 설정
- 일반적으로 제목을 포함해서 의미를 가진다
- [MDN: <section>](https://developer.mozilla.org/ko/docs/Web/HTML/Element/section)
<br/><br/>

```html
<article> vs <section> vs <div>
모두 구획하는 역할을 하지만 <div>는 의미가 없고 <section>은 포함된 제목을 통해 의미를 가진다.
그리고 <article>은 독립적으로 구분되고 제목을 통해 의미를 가진다.
```
<br/>

### <aside>
- \<aside\>는 문서의 별도 콘텐츠(광고나 기타 링크 등의 사이드바 등)를 설정
- [MDN: <aside>](https://developer.mozilla.org/ko/docs/Web/HTML/Element/aside)
<br/><br/>

### <nav>
- \<nav\>는 다른 페이지 링크를 제공하는 영역을 설정
- 보통 메뉴(Home, About, Contact), 목차, 색인 등의 영역을 설정
- 주로 \<ol\> 혹은 \<ul\>과 같이 쓰인다.
- [MDN: <nav>](https://developer.mozilla.org/ko/docs/Web/HTML/Element/nav)
<br/><br/>

### <address>
- \<address\>는 연락처 정보(주소, 전화번호, 이메일 주소 등)을 제공하는 영역을 설정
- [MDN: <address>](https://developer.mozilla.org/ko/docs/Web/HTML/Element/address)
<br/><br/>

### <div>
- \<div\>는 아무것도 나타내지 않는 콘텐츠 영역을 설정
- 주로 css를 통해 꾸미거나 JS를 통해 제어하기 위해 사용
- [MDN: <div>](https://developer.mozilla.org/ko/docs/Web/HTML/Element/div)
<br/><br/><br/><br/>

## 2. 문자 콘텐츠 요소
### <ol>, <ul>, <li>
- \<ol\>, \<ul\>, \<li\>은 목록을 만드는 태그
- 각각 ordered list(순서가 필요한 목록), unordered list(순서가 필요없는 목록), list item을 의미
- \<ol\>과 \<ul\>은 자식 요소로 \<li\>만 포함 가능
- \<li\>는 \<ol\> 혹은 \<ul\>의 자식으로 포함되어야만 사용 가능
- \<ol\>의 항목 순서는 중요도를 의미할 수 있음

✨ 일반적으로 \<ol\>보다 \<ul\>을 많이 사용한다.
<br/><br/>

### <dl>, <dt>, <dd>
- 용어 (\<dt\>)와 정의 (\<dd\>) 쌍들(리스트)의 영역(\<dl\>)을 설정
- \<dl\>, \<dt\>, \<dd\>은 각각 Definition list, Definition Term, Definition Details를 의미
- \<dl\>은 \<dt\>와 \<dd\>만 자식 요소로 가질 수 있다
- Key, Value 형태를 표시할 때 유용하다 (용어-설명 ⇒ key-value)

✨ \<dl\>은 자식 요소로 \<dt\>와 \<dd\>만 가질 수 있기 때문에 꾸미기 까다롭다. 그래서 일반적으로 <ul> + <li> + <p> 로 대체해서 사용한다.
<br/><br/>

### <p>, <hr>
- \<p\>는 paragraph를 의미하며 하나의 문단을 설정하기 위해 사용
- \<p\> 태그 내부에 있는 텍스트는 줄바꿈 혹은 탭이 적용 X
- \<hr\>은 self-closing tag이며 horizontal rule을 의미
- \<hr\>은 문단을 분리하기 위해 사용
- \<hr\>을 시각적 관점에서 수평선(border)을 표시하기 위해 사용하지 말고 의미적 관점에서 문단을 분리하기 위해 사용
<br/><br/>

### <pre>
- \<pre\>는 Preformatted Text 이라는 뜻
- 서식이 미리 지정된 텍스트를 설정
- 문자가 입력된 그대로 보여진다
- 기본적으로 문자들의 가로 길이가 같은 Monospace 글꼴 계열로 표시
- \<pre\>는 시작하는 그 부분부터 그대로 보여지기 때문에 텍스트 앞, 뒤에 <pre> 태그를 딱 붙여야 한다

✨ 사용자가 '입력한 그대로' 보여주고 싶을 때 주로 사용 (블로그에 코드 올릴 때 등)
<br/><br/>

### <blockquote>
- \<blockquote\>는 Block Quotation의 약어
- 일반적인 인용문을 설정하기 위해 사용
<br/><br/><br/><br/>  

## 3. Refernece
- [HEROPY Tech - 한눈에 보는 HTML 요소(Elements & Attributes) 총정리](https://heropy.blog/2019/05/26/html-elements/)
<br/><br/><br/><br/>