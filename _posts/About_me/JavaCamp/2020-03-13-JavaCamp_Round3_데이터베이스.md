---
layout: post
title: "[Java-GUI] ROUND3. 데이터베이스 연결"
date: 2020-03-14
categories: JavaCamp
tags: about java gui database mysql
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
- [[Java-GUI] ROUND3. 번외 ) Eclipse Java - MySQL 연동](https://0pencoding.github.io/about/java/gui/database/mysql/2020/03/14/13-JavaCamp_Round3.5_%EC%9E%90%EB%B0%94MySQL%EC%97%B0%EA%B2%B0.html)
- [[JAVA] MySQL 조회, 쓰기, 수정, 삭제](https://goppa.tistory.com/entry/MySQL-%EC%A1%B0%ED%9A%8C-%EC%93%B0%EA%B8%B0-%EC%88%98%EC%A0%95-%EC%82%AD%EC%A0%9C)
<br/><br/><br/>

## 3. 결과물
<br/>
![database](/assets/img/post/About_me/JavaCamp/database.png){:width="250px"}  

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
ㅤ![database_detail](/assets/img/post/About_me/JavaCamp/database_detail(1).png){:width="700px"}  
<br/>
ㅤ![database_detail](/assets/img/post/About_me/JavaCamp/database_detail(2).png){:width="700px"}  
<br/>
ㅤ![database_detail](/assets/img/post/About_me/JavaCamp/database_detail(3).png){:width="800px"}
<br/><br/><br/>

## 5. 코드 세부 설명
<br/>
![database_uml](/assets/img/post/About_me/JavaCamp/database_uml.gif){:width="1000px"}  

위 사진은 내 코드를 UML Diagram으로 나타낸 것이다.  
점점 객체지향 언어인 Java에 맞게 그럴싸하게 class 별로 코드를 짜도록 성장하는 것 같다.  
클래스가 너무 많아 사진이 잘 안보일 수 있을 것 같은데 사진을 다운받아서 확대시켜 보면 크게 볼 수 있을 것이다.  

코드를 세부적으로 설명하면 아래와 같다.
- **`Main class`** : MySQL과 연결시키고, 모든 display 화면들을 멤버로 가져 navigation을 담당하는 클래스
    - **`Main()`** : Frame을 설정해서 첫 화면을 보여주고 모든 display 각각에 맞는 ActionListener를 설정
    - **`actionPerformed()`** : 누른 버튼에 따라 그것에 맞는 행동을 하는 함수들을 설정
    - **`나머지 함수들`** : 누른 버튼에 따라 그것에 맞는 행동들을 하는 함수들
- **`InitDisplay class`** : 처음에 어플리케이션을 켰을 때 화면
    - **`InitDisplay()`** : 첫 화면의 Panel을 설정하고 가입하기 버튼과 로그인 버튼을 세팅
- **`Join class`** : 가입하기 화면
    - **`Join()`** : 가입하기 화면의 Panel을 설정하고 ID, PW, Nickname을 입력할 수 있는 textField 와 확인 버튼들 세팅
- **`Login class`** : 로그인 화면
    - **`Login()`** : 로그인 화면의 Panel을 설정하고 ID와 PW를 입력할 수 있는 textField 와 로그인 버튼 세팅
- **`Menu class`** : 내 정보를 보거나 수정, 조회, 로그아웃, 탈퇴를 할 수 있는 메뉴 화면
    - **`Menu()`** : 내 정보 조회, 수정, 로그아웃, 탈퇴를 할 수 있는 버튼 세팅
- **`MyInfo class`** : 내 정보를 보여주는 화면
    - **`MyInfo()`** : 나의 정보를 보여줄 수 있도록 화면 세팅
- **`Edit class`** : 내 정보를 수정할 수 있는 화면
    - **`Edit()`** : 내 정보를 수정할 수 있도록 하는 버튼들과 수정하고 각 버튼들을 눌렀을 경우 ActionListener 추가
    - **`actionPerformed()`** : 내 정보를 수정할 수 있도록 하는 버튼들을 눌렀을 경우 각각에 맞는 행동들을 수행
- **`Search class`** : 내 정보를 조회 할 수 있는 화면
    - **`Search()`** : 내 정보를 조회하는 버튼들과 세팅
- **`나머지 클래스들`** : 가입이나 로그인, 개인 정보를 수정할 때에 ID, PW의 조건에 맞게 설정했는지를 알려주는 Frame들

UML Diagram을 보면 알겠지만, 주요 클래스와 함수들만 설명했다.  
하나하나 전부 설명하기에는 너무 내용이 많고 쓸데없는 설명들까지 되기에 필요한 부분들만 설명했다.  
혹시 코드를 보고 궁금한 점이나 문의할 내용이 있으면 댓글로 남겨주세요!
<br/><br/><br/>

## 6. GitHub 및 프로젝트 보고서
제 코드는 아래 GitHub에서 확인 가능합니다 :)  
<https://github.com/0pencoding/JavaCamp-Round3-Database>

또한 위 코드 설명보다 더 자세한 설명이나 실행 결과가 필요하다면 아래 링크에서 보고서를 다운받을 수 있습니다 :)  
<https://drive.google.com/file/d/1jKqC_JaYrER1g6qOag4Q68FpDpJwpHKO/view?usp=sharing>
<br/><br/><br/>

## [[Round 4] 이미지 프로세싱 구현 ➜ ](https://0pencoding.github.io/about/java/gui/imageprocessing/2020/03/14/JavaCamp_Round4_%EC%9D%B4%EB%AF%B8%EC%A7%80%ED%94%84%EB%A1%9C%EC%84%B8%EC%8B%B1.html)
{: style="text-align: right;"}
<br/>