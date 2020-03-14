---
layout: post
title: "[Java-GUI] ROUND5. 육목 만들기"
date: 2020-03-14
categories: About Java GUI
sitemap:
    changefreq: daily
---

벌써 2주일이 넘었다. 이제 프로젝트도 2개만 남겨두고있는 상태인데, 사실상 프로젝트는 한 개만 남은거라고 생각해도 무방할 것 같다. 이번 프로젝트인 육목은 다음 프로젝트인 네트워크 육목을 위한 준비과정이라고 할 수 있기 때문이다. 그럼 다음 프로젝트를 위해서 기반을 잘 마련해보자. 프로젝트를 진행하지 않는 사람들에게는 나의 코드와 설명이 유용한 정보가 되길 바란다 :)  
<br/>

<br/>
### ⏰ 기간 ⏰ㅤ2일
<br/>

## 1. 기능
* 두 명의 플레이어가 육목 게임이 가능하도록 구현
* 이외에는 자유롭게 자신이 선보이고 싶은 기능, 있으면 좋겠다 싶은 기능 추가
<br/><br/><br/>

## 2. 시작!
지금까지 4개의 프로젝트를 해오면서 Java GUI에 대해서는 꽤나 익숙해졌을 것 같다.  
따라서 이번 프로젝트는 새로운 개념을 익혀야 하는 것도 아니기 때문에 2일 동안 빠르게 구현해 보도록 하자.   
사실상 자신이 어떻게 구현할지에 따라 필요한 자료는 많이 달라지기 때문에 제공할 수 있는 Reference는 육목 규칙 정도이다.  
또한 육목에관한 Reference는 많지 않기 때문에 오목에 관련해서 찾아보고 로직만 자신이 구현하면 될 것 같다.  
Reference 아래로는 나의 결과물과 설명이 이어진다.  
꼭 2일 후에 본 프로젝트를 마무리하고 확인하길 바란다.  
그냥 내 코드와 결과물을 보고 공부한다면 그것도 물론 공부가 되겠지만 자신이 직접 찾아가며 한 공부보다는 훨씬 못할 것이다.  
또한 말했듯이 그 당시에는 몰랐지만 지금보면 내 코드도 잘 짜여진 코드는 아님을 참고해주었으면 좋겠다 (-﹏-。;)  

### Reference
- [육목](https://namu.wiki/w/%EC%9C%A1%EB%AA%A9)
- [자바 오목게임 만들기](https://message0412.tistory.com/entry/%EC%9E%90%EB%B0%94-%EC%98%A4%EB%AA%A9%EA%B2%8C%EC%9E%84-%EB%A7%8C%EB%93%A4%EA%B8%B0)
<br/><br/><br/>

## 3. 결과물
<br/>
![connect6](/assets/img/post/About_me/JavaCamp/connect6.png){:width="800px"}  

### 구현 기능
- 두 명의 플레이어가 육목 게임이 가능하도록 구현
- 각 플레이어의 이름과 캐릭터를 설정
- 한 턴의 시간을 정해놓고 시간이 지나면 다른 플레이어의 순서로 넘어가게 구현
- 배경 노래 삽입

### 보완 해야할 부분
- restart 했을 경우 음소거되었던 배경 노래가 다시 시작하는 문제
- restart 했을 경우 시작하기 전에 시간이 흘러가는 문제
- 게임의 시작 부분으로 넘어갈 수 있는 Go Home 버튼 추가
- 일시정지 기능 추가
<br/><br/><br/>

## 4. 세부 기능 캡쳐
<br/>
ㅤ![connect6_detail](/assets/img/post/About_me/JavaCamp/connect6_detail.png){:width="900px"}
<br/><br/><br/>

## 5. 코드 세부 설명
<br/>
![connect6_uml](/assets/img/post/About_me/JavaCamp/connect6_uml.gif){:width="750px"}  

위 사진은 내 코드를 UML Diagram으로 나타낸 것이다.  
좀 더 잘짜면 객체 지향 언어의 장점인 재사용을 이용해서 코드를 간단하게 할 수 있을 것 같은데,  
다음에 시간과 기회가 된다면 코드를 refactoring 해야겠다.

코드를 세부적으로 설명하면 아래와 같다.
- **`Main class`** : Screen1, Screen2, Screen3 화면들의 navigation을 담당하는 클래스
    - **`Main()`** : Frame을 설정해서 첫 화면을 보여주고 모든 Screen 각각에 맞는 ActionListener를 설정
    - **`actionPerformed()`** : 누른 버튼에 따라 그것에 맞는 행동을 하는 함수들을 설정
    - **`나머지 함수들`** : 누른 버튼에 따라 그것에 맞는 행동들을 하는 함수들
- **`Screen1 class`** : 처음에 어플리케이션을 켰을 때 화면
    - **`Screen1()`** : 첫 화면의 Panel을 설정하고 시작하기 버튼 세팅
- **`Screen2 class`** : 두 플레이어의 이름과 캐릭터를 설정하는 화면
    - **`Screen2()`** : 플레이어의 이름과 캐릭터를 설정할 수 있는 이미지와 TextField 세팅
- **`Screen3 class`** : 실제로 게임을 진행하는 화면
    - **`Screen3()`** : 게임 진행을 위한 각 플레이어의 Panel을 설정하고 게임 진행 상황에 맞게 게임판을 다시 그려줄 수 있도록 MouseListener 추가
- **`Board class`** : 게임의 진행과정을 보여주는 실질적인 게임판으로, 플레이어의 이벤트에 따라 적절한 행동을 취하는 클래스
    - **`Board()`** : 게임판을 그리고 플레이어의 이벤트에 따라 알맞은 행동을 하도록 MouseListener 추가
    - **`paintComponent()`** : 플레이어가 돌을 둘 때마다 게임판을 다시 그려주는 역할
    - **`나머지 함수들`** : 게임 진행을 위해 어느 플레이어의 차례이고, 게임이 끝났는지를 확인해주는 함수들
- **`Player1Panel class`** : Player1의 캐릭터와 이름을 보여주고 게임 진행 상황을 정보와 상황을 표시하는 Panel
- **`Player2Panel class`** : Player2의 캐릭터와 이름을 보여주고 게임 진행 상황을 정보와 상황을 표시하는 Panel, 또한 Background music을 제어할 수 있는 부분 포함
- **`Player class`** : Player의 캐릭터와 이름을 저장하는 객체
- **`WinPanel class`** : 게임에서 이긴 플레이어를 표시해주는 Panel
- **`BackgroundSound class`** : Background music을 제어하는 클래스




UML Diagram을 보면 알겠지만, 주요 클래스와 함수들만 설명했다.  
혹시 코드를 보고 궁금한 점이나 문의할 내용이 있으면 댓글로 남겨주세요!
<br/><br/><br/>

## 6. GitHub 및 프로젝트 보고서
제 코드는 아래 GitHub에서 확인 가능합니다 :)  
(배경음악은 파일이 너무 커서 올리지 못했습니다. 실행하시면 소리는 나지 않을거예요!)  
<https://github.com/0pencoding/JavaCamp-Round5-Connect6>
<br/><br/><br/>

<!-- ## [[Round 6] 육목 네트워크 적용 ➜ ](abc)
{: style="text-align: right;"}
<br/> -->