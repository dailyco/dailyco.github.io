---
layout: post
title: "[Java-GUI] ROUND6. 육목 네트워크 적용하기"
date: 2020-03-14
categories: JavaCamp
tags: about java gui network socketprogramming
sitemap:
    changefreq: daily
---

드디어 마지막이다. 길었다면 길고 짧았다면 짧은 6개의 프로젝트가 거의 막을 내리고있다. 여기까지 포기하지않고 온 사람들에게는 정말 대단하고 수고했다고 박수쳐주고싶다. 그럼 마지막까지 잘 마무리 짓길 바라면서, 이번 프로젝트는 [이전 라운드](https://0pencoding.github.io/about/java/gui/2020/03/14/JavaCamp_Round5_%EC%9C%A1%EB%AA%A9.html)에서 구현했던 육목에 네트워크를 적용시켜 실제로 두 플레이어가 육목 게임이 가능하도록 하는 것이다. 프로젝트를 진행하지 않는 사람들에게는 나의 코드와 설명이 유용한 정보가 되길 바란다 :)  
<br/>

<br/>
### ⏰ 기간 ⏰ㅤ4일
<br/>

## 1. 기능
* 서로 다른 컴퓨터에서 육목 게임이 가능하도록 네트워크를 연결
* 이외에는 자유롭게 자신이 선보이고 싶은 기능, 있으면 좋겠다 싶은 기능 추가
<br/><br/><br/>

## 2. 시작!
마지막 프로젝트인만큼 끝까지 잘 마무리 지었으면 좋겠다.  
이번 프로젝트에서는 네트워크와 관련해서 특히 소켓프로그래밍, TCP 개념에 대해 공부해야할 것이다.  
내가 프로젝트를 진행했을 당시에는 개념이 너무 어려워서 이해하지않고 그냥 사용했었는데,  
네트워크 수업을 듣고 다시보니 그럭저럭 이해가되는 것 같다.  
Reference 자료 외에도 더 많이 찾아보면서 개념을 익히고 네트워크를 잘 연결시켰으면 좋겠다.  
Reference 아래로는 나의 결과물과 설명이 이어진다.  
꼭 4일 후에 본 프로젝트를 마무리하고 확인하길 바란다.  
그냥 내 코드와 결과물을 보고 공부한다면 그것도 물론 공부가 되겠지만 자신이 직접 찾아가며 한 공부보다는 훨씬 못할 것이다.  
또한 말했듯이 그 당시에는 몰랐지만 지금보면 내 코드도 잘 짜여진 코드는 아님을 참고해주었으면 좋겠다 (-﹏-。;)  

### Reference
- [[Java] 자바 네트워크에 대한 이해](https://coding-factory.tistory.com/267)
- [[Java] 자바 네트워크 TCP 통신 소켓프로그래밍](https://coding-factory.tistory.com/270)
<br/><br/><br/>

## 3. 결과물
<br/>
![network_connect6](/assets/img/post/About_me/JavaCamp/connect6.png){:width="800px"}  

### 구현 기능
- 서로 다른 컴퓨터에서 육목 게임이 가능하도록 네트워크를 연결
- 이전 육목 프로젝트에서 더해진 기능으로는 여러 사람이 대전할 수 있도록 6개의 방 생성

### 보완 해야할 부분
- 일시정지하는 기능
- Player의 이름이 같은지 중복 확인
- 방을 6개로 한정짓지말고 방을 만들수 있도록
- 대기방에서 현재 방에 몇 명이 대기중인지 표시해주도록
- 게임도중 플레이어가 퇴장했을 경우 다른플레이어에게 알려주기
- 방에 입장해서 게임 시작하기 버튼을 눌렀을 때 상대방에게 메세지 표시해주기
<br/><br/><br/>

## 4. 세부 기능 캡쳐
<br/>
ㅤ![network_connect6_detail](/assets/img/post/About_me/JavaCamp/network_connect6_detail(1).png){:width="700px"}  
<br/>
ㅤ![network_connect6_detail](/assets/img/post/About_me/JavaCamp/network_connect6_detail(2).png){:width="700px"}
<br/><br/><br/>

## 5. 코드 세부 설명
<br/>
![network_connect6_uml](/assets/img/post/About_me/JavaCamp/network_connect6_uml.gif){:width="800px"}  

위 사진은 내 코드를 UML Diagram으로 나타낸 것이다.  
클래스가 너무 많아 사진이 잘 안보일 수 있을 것 같은데 사진을 다운받아서 확대시켜 보면 크게 볼 수 있을 것이다.  

코드를 세부적으로 설명하면 아래와 같다.  
이전 프로젝트와 중복되는 부분의 설명은 하지 않았으니 그 부분이 궁금한 사람들은 [**여기**](https://0pencoding.github.io/about/java/gui/2020/03/14/JavaCamp_Round5_%EC%9C%A1%EB%AA%A9.html) 에서 확인하면 될 것 같다.

- **`MainServer class`** : TCP 서버 소켓을 생성해 실행시키면서 Client 접속시 관리해주는 클래스
    - **`startServer()`** : TCP 서버소켓을 생성해 Client의 접속을 감지하고 Thread를 사용해서 관리해주는 역할
    - **`GameThread class`** : Client가 접속될 때마다 생성되어 플레이어를 관리해주는 역할
    - **`Manager class`** : 전체적으로 방을 관리해주는 클래스로 방이 꽉찼는지 게임 준비 상태인지 등을 관리해주는 역할
- **`MainClient class`** : 이전 프로젝트의 Main class와 같은 역할
- **`Screen3 class`** : 대기방 화면
- **`Screen4 class`** : 방 입장시 상대 플레이어 대기 화면
- **`Screen5 class`** : 실제적인 게임이 이루어지는 화면으로 이전 프로젝트의 Screen3와 같은 역할


UML Diagram을 보면 알겠지만, 주요 클래스와 함수들만 설명했다.  
혹시 코드를 보고 궁금한 점이나 문의할 내용이 있으면 댓글로 남겨주세요!
<br/><br/><br/>

## 6. GitHub 및 프로젝트 보고서
제 코드는 아래 GitHub에서 확인 가능합니다 :)  
(배경음악은 파일이 너무 커서 올리지 못했습니다. 실행하시면 소리는 나지 않을거예요!)  
<https://github.com/0pencoding/JavaCamp-Round6-NetworkConnect6>
<br/><br/>