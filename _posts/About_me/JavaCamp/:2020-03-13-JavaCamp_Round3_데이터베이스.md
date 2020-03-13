---
layout: post
title: "[Java-GUI] ROUND3. 데이터베이스 연결"
date: 2020-03-14
categories: About Java GUI Database MySQL
sitemap:
    changefreq: daily
---

벌써 일주일이 넘었다. 'Round2 그림판 만들기' 를 하면서 Java GUI를 능숙하게 다룰 수 있다는 자신감을 가졌길 바라며, 다음 단계로 넘어가 보자! 세번째 프로젝트는 데이터베이스이다. 데이터베이스에 대해서 알고있는 사람도 있을 것이고 모르는 사람도 있을텐데 다행이도(?) 자바와 MySQL을 Eclipse를 사용해 연결시키는 과정은 내가 정리할 계획이다. 프로젝트를 진행하지 않는 사람들에게는 나의 코드와 설명이 유용한 정보가 되길 바란다 :)  
<br/>

<br/>
### ⏰ 기간 ⏰ㅤ3일
<br/>

## 1. 기능
* 신규 가입 (ID 중복 확인, PW 확인)
* 로그인 (ID, PW 확인)
* 로그인 후 개인 정보 수정, 탈퇴
* Admin모드 (Optional)
* 이외에 자유롭게 자신이 선보이고 싶은 기능, 있으면 좋겠다 싶은 기능 추가
<br/><br/><br/>

## 2. 시작!
데이터베이스에 대한 기본 개념이 잡혀있지 않은 사람들에게는 본 프로젝트가 조금 버거울 수 있다.  
따라서 Reference에서 Eclipse를 사용해 자바와 데이터베이스를 연결하는 방법에 대해서 공부하길 바란다.  
또한 내가 제공하는 자료는 정말 한정적이기 때문에 필요한 자료는 더 열심히 찾고 공부해야한다.  
이번에도 Reference 아래로는 나의 결과물과 설명이 이어진다.  
꼭 3일 후에 본 프로젝트를 마무리하고 확인하길 바란다.  
그냥 내 코드와 결과물을 보고 공부한다면 그것도 물론 공부가 되겠지만 자신이 직접 찾아가며 한 공부보다는 훨씬 못할 것이다.  
이전에도 말했듯이 그 당시에는 몰랐지만 지금보면 내 코드도 잘 짜여진 코드는 아님을 참고해주었으면 좋겠다 (-﹏-。;)  

### Reference
- [[Java-GUI] ROUND3. 번외 ) Eclipse Java - MySQL 연동]()
- 
<br/><br/><br/>

## 3. 결과물
<br/>
![database](/assets/img/post/About_me/JavaCamp/database.png){:width="750px"}  

### 구현 기능
- 신규 가입 (ID 중복 확인, PW 확인)
- 로그인 (ID, PW 확인)
- 개인 정보 수정, 조회, 탈퇴, 로그아웃
- 성별 수정 및 보여지는 기능

### 보완 해야할 부분
- Admin 모드
- 이름이 보여지는 부분을 이름 길이에 맞게 조정
<br/><br/><br/>

## 4. 세부 기능 캡쳐
<br/>
ㅤ![database_detail](/assets/img/post/About_me/JavaCamp/database.png){:width="400px"}  
<br/><br/><br/>

## 5. 코드 세부 설명
<br/>
![database_uml](/assets/img/post/About_me/JavaCamp/database_uml.gif){:width="900px"}  

위 사진은 내 코드를 UML Diagram으로 나타낸 것이다.  
점점 객체지향 언어인 Java에 맞게 그럴싸하게 class 별로 코드를 짜도록 성장하는 것 같다.  

코드를 세부적으로 설명하면 아래와 같다.
- **`Main class`** : 
    - **`Main()`** : 

UML Diagram을 보면 알겠지만, 주요 클래스와 함수들만 설명했다.  
혹시 코드를 보고 궁금한 점이나 문의할 내용이 있으면 댓글로 남겨주세요!
<br/><br/><br/>

## 6. GitHub 및 프로젝트 보고서
제 코드는 아래 GitHub에서 확인 가능합니다 :)  
<https://github.com/0pencoding/JavaCamp-Round2-DrawBoard>

또한 위 코드 설명보다 더 자세한 설명이나 실행 결과가 필요하다면 아래 링크에서 보고서를 다운받을 수 있습니다 :)  
<https://drive.google.com/file/d/15mE3ce3AQZ2JYinjSA9cl54PlF53mcJc/view?usp=sharing>
<br/><br/><br/>

<!-- ## [[Round 4] 이미지 프로세싱 구현 ➜ ](abc)
{: style="text-align: right;"}
<br/> -->