---
layout: post
title: "WEB Front-end 공부 일기 : HTML 개요 및 요소"
date: 2020-07-18
categories: Front-end
tags: web front study html
sitemap:
    changefreq: daily
---

공부를 시작한지 이틀째 되는 날이었다. 본격적으로 HTML 공부에 들어갔고, 전체적인 개요부터 시작해서 어떤 요소들이 있고, 요소마다 특성들에 대해 배우기 시작했다. HTML을 제대로 공부해본적이 없기도하고, 웹과 관련된 수업을 학교에서도 한 번도 들어본적이 없어서 조금 낯설게 느껴졌지만 평소에 무척 공부해보고 싶었던 분야라서 재미있게 들은것 같다 :)  
<br/>

<br/>

### 💡알림💡
본 일기는 패스트 캠프의 '프론트엔드 개발 올인원 패키지 with React Online' 강의를 기반으로 공부한 내용을 복습할 목적으로 작성함을 밝히며, 잘못된 부분이 존재할 수도 있음을 알립니다! 잘못된 부분은 댓글로 말씀해주시면 감사하겠습니다 ʕ•̀ω•́ʔ✧
<br/><br/>

### ⏰ㅤWEB Front-end 공부 일기 2
먼저는 HTML 태그에는 어떤 종류가 있는지 전체적인 개요를 알아보고, 블록 요소와 인라인 요소들에 대해서 배우면서 무엇이 다른지 그 특성에 대해 알아보았다. 그리고 구체적으로 요소를 하나씩 알아보면서 어디에 쓰는 요소이고 어떤 속성과 특성을 가지는지 공부했다.
<br/><br/><br/>

## 1. HTML 요소 개요

```html
<!DOCTYPE html>
<html lang="ko">
    <head>
        문서의 정보
        <!-- 기타 정보 -->
        <meta charset="UTF-8" name content>
        <meta name="author" content="YJ">
        <meta name="description" content="YJ's blog">
        <meta http-equiv="X-UA-Compatible" content="IE=edge"> <!-- 최신 IE 지원하도록 -->
        
        <!-- HTML 문서 제목 -->
        <title>HTML 요소 레퍼런스</title>

        <!-- 기본 파일의 경로 설정 -->
        <base href="./css/">
        <!-- 스타일 외부에서 가져와서 연결 -->
        <link rel="stylesheet" href="main.css">

        <!-- 스타일 직접 입력 -->
        <style type="text/css">
                div {
                    color: red;
                    background: blue;
                }
        </style>
    </head>

    <body>
            문서의 구조
    </body>
</html>
```
<br/>

- `<!DOCTYPE html>`  
html5 버전으로 해석해서 브라우저에 표현
<br/>

- `<html lang="ko, en...">...</html>`  
html 문서로 작성함을 표현하며 어느 나라 언어를 사용하는지 설정
<br/>

- `<head>...</head>` 문서의 정보
    - [`<meta>`](https://developer.mozilla.org/ko/docs/Web/HTML/Element/meta) 속성
        - `charset`: 페이지의 문자의 인코딩 방법
        - `content`: `name`, `http-equiv` 속성을 사용할 때 해당 속성의 값을 입력
        - `http-equiv`: 렌더링 방식 등 서버나 사용자의 환경에 맞게 작동 방식을 변경시키는 지시 사항 명시
        - `name`: 문서 레벨의 메타 데이터 이름 정의 (정보를 지칭할 때 그 정보가 무엇인지)
            - author, description, viewport,  ...
    - [`<link>`](https://developer.mozilla.org/ko/docs/Web/HTML/Element/link) 속성  
        현재 문서와 외부 리소스와의 관계 명시 (가지고 오는 것 까지)  
        - `crossorigin` 다른 도메인 사이트와 정보를 어떻게 주고 받을지를 명시(?)
        - `href` 링크된 리소스의 URL (절대/상대 경로)
        - `hreflang` 링크된 리소스의 언어 (보통 생략)
        - `rel` 링크된 문서와 현재 문서와의 관계 명명
            - 링크 타입 값: stylesheet, icon, ...
        - `type` : css의 경우 생략 가능
            - [MIME type](https://developer.mozilla.org/ko/docs/Web/HTTP/Basics_of_HTTP/MIME_types)

    - [`<style>`](https://developer.mozilla.org/ko/docs/Web/HTML/Element/style) 속성
        - `type` : 생략 가능 (ex. type = "text/css")

    - `<base>`
        - 주의: html 문서에 한 번만 사용 가능
<br/><br/>

- `<body>...</body>` 문서의 구조  
HTML 문서 구조의 정보를 표현
<br/><br/><br/><br/>

## 2. 블록 / 인라인 요소
### 블록 요소
header, footer, h1~h6, main, article, section, aside, nav, address, div, ol, ul, dl, dt, dd, p, hr, pre, blockquote, figure, form
<br/><br/>

### 인라인 요소
a, abbr, b, mark, em, strong, i, dfn, cite, q, u, code, kbd, sup, sub, time, span, br, del, ins, img, audio, video, figcaption, iframe, canvas, noscript
<br/><br/><br/><br/>

## 3. 블록 / 인라인 요소의 특성
### 블록 요소
1. 사용 가능한 최대 가로 너비를 사용
2. 크기를 지정할 수 있다
3. width: 100%, height: 0 에서 시작
4. 수직으로 쌓인다
5. margin과 padding의 위, 아래, 좌, 우 모두 사용 가능
6. 레이아웃 작업
<br/><br/>

### 인라인 요소
1. 필요한 만큼의 너비만 사용
2. 크기를 지정할 수 없다
3. width: 0, height: 0 에서 시작
4. 수평으로 쌓인다  
(줄바꿈을 하면 오른쪽으로 약간의 여백이 들어가고, 줄바꿈을 하지 않으면 여백 없이 그대로 옆으로 쭉 이어진다)
5. margin, padding의 위, 아래는 사용 할 수 없다  
(padding 위, 아래가 들어간 것 처럼 보이나 아래에 다른 요소들이 있을 경우 실제로는 그 위에 덮어 씌워짐)
6. TEXT 작업
<br/><br/>

### 블록 / 인라인 요소의 특성을 가져다 쓰기
```css
display: inline
display: block
```

블록 요소의 경우의 위의 코드 처럼 `display: inline` 을 사용해서 인라인 요소 처럼 (인라인 요소의 특성을 적용) 사용할 수 있으며,  
인라인 요소의 경우도 마찬가지로 `display: block` 을 사용해서 블록 요소처럼 (블록 요소의 특성을 적용) 사용 할 수 있다.
<br/><br/><br/><br/>

## 4. Refernece
- [HEROPY Tech - 한눈에 보는 HTML 요소(Elements & Attributes) 총정리](https://heropy.blog/2019/05/26/html-elements/)
<br/><br/><br/><br/>