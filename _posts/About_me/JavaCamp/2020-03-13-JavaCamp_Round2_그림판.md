---
layout: post
title: "[Java-GUI] ROUND2. 그림판 만들기"
date: 2020-03-13
categories: About Java GUI Graphics
sitemap:
    changefreq: daily
---

첫 실전을 마무리했다. 'Round1 계산기 만들기' 에서 Java GUI에 대해서 조금 감을 잡았길 바라며, 다음 단계로 넘어가 보자! 두번째 프로젝트는 그림판이다. Round1에서는 GUI에 대해 익히는 것이었다면 이번 라운드에서는 java GUI를 좀 더 깊게 공부하게 되지 않을까 생각한다. 마찬가지로 프로젝트를 진행하지 않는 사람들에게는 나의 코드가 유용한 정보가 되길 바란다 :)  
<br/>

<br/>
### ⏰ 기간 ⏰ㅤ4일
<br/>

## 1. 기능
* 그리기: 선, 사각형, 원, Polyline, Sketch(Pen), Spray, Pattern 中 최소 4가지 이상 필수 선택
* 속성: 굵기, 색, Style, 채우기 中 최소 2가지 이상 필수 선택
* 부가기능: drag & drop, resize, rotate, undo/redo, 지우기, 저장/불러오기, 복사/붙여넣기, grouping/ungrouping  
中 최소 2가지 이상 필수 선택
* 이외에 자유롭게 자신이 선보이고 싶은 기능, 있으면 좋겠다 싶은 기능 추가
<br/><br/><br/>

## 2. 시작!
마찬가지로 검색을 좀 더 수월하게 하기위해 약간의 Reference를 제공한다.  
하지만 말했듯이 내가 제공하는 자료는 정말 한정적이기 때문에 필요한 자료는 더 열심히 찾고 공부해야한다.  
Reference 아래로는 나의 결과물과 설명이 이어진다.  
꼭 4일 후에 본 프로젝트를 마무리하고 확인하길 바란다.  
그냥 내 코드와 결과물을 보고 공부한다면 그것도 물론 공부가 되겠지만 자신이 직접 찾아가며 한 공부보다는 훨씬 못할 것이다.  
또한 역시 말했듯이 그 당시에는 몰랐지만 지금보면 내 코드도 잘 짜여진 코드는 아니다 (-﹏-。;)  

### Reference
- [자바 GUI Graphics (그래픽) 그리기 기초](https://aiden1004.tistory.com/entry/%EC%9E%90%EB%B0%94-GUI-%EA%B7%B8%EB%9E%98%ED%94%BD-%EA%B7%B8%EB%A6%AC%EA%B8%B0-%EA%B8%B0%EC%B4%88)
- [자바GUI강의 8.[패널에 그림그리기]](https://blog.naver.com/khk6435/50112360444)
<br/><br/><br/>

## 3. 결과물
<br/>
![drawboard](/assets/img/post/About_me/JavaCamp/drawboard.png){:width="750px"}  

### 구현 기능
- 그리기: 선, 사각형, 원, Sketch(Pen)
- 속성: 굵기, 색
- 부가 기능: undo/redo, 지우기, 저장/불러오기
- 나만의 기능: 텍스트 모드, 캔버스 여러개, 캔버스 삭제

### 보완 해야할 부분
- 텍스트 모드에서 클릭하면 글 쓰기를 시작할 수 있게
- 텍스트 모드에서 txt 파일이 저장되도록
- 캔버스 별로 메모리가 분리 되도록
- 지우개 사용할 때 지우개의 크기를 알 수 있도록
- 파일을 불러왔을 때 수정 가능하도록
<br/><br/><br/>

## 4. 세부 기능 캡쳐
<br/>
ㅤ![calculator_detail](/assets/img/post/About_me/JavaCamp/drawboard_detail(1).png){:width="400px"}  

ㅤ![calculator_detail](/assets/img/post/About_me/JavaCamp/drawboard_detail(2).png){:width="700px"}
<br/><br/><br/>

## 5. 코드 세부 설명
<br/>
![calculator_uml](/assets/img/post/About_me/JavaCamp/drawboard_uml.gif){:width="900px"}  

위 사진은 내 코드를 UML Diagram으로 나타낸 것이다.  
그래도 처음 계산기에 비하면 나름 class 별로 짜려고 노력한 흔적이 보인다.  

코드를 세부적으로 설명하면 아래와 같다.
- **`Main class`** : Drawboard의 전체적인 큰 프레임
    - **`Main()`** : Frame의 제목, 크기를 설정해주고, 닫기를 눌렀을 때 닫아지도록 설정, 또한 MenuBar와 ToolBar, Canvas 탭을 추가
- **`MenuBar class`** : 프레임의 메뉴바 부분
    - **`MenuBar()`** : 저장과 불러오기를 만들고 여기에 각각 알맞은 ActionListener를 더해주는 역할
    - **`actionPerformed()`** : 저장과 불러오기를 눌렀을 때 각각 JFileChoose를 사용해서 해당 이벤트를 실행
- **`ToolBar class`** : 프레임의 메뉴바 아래에 툴바 부분
    - **`ToolBar()`** : 툴바의 배경색을 설정하고, 툴바에 Buttons 클래스를 추가해 툴바를 완성
- **`Buttons class`** : 툴바의 버튼들을 구성
    - **`Buttons()`** : 툴바에 필요한 버튼들을 생성하고 각 버튼들에 MouseListener를 추가
    - **`moustClicked()`** : 툴바의 각 버튼들을 눌렀을 때 해당 버튼에 맞는 행동들을 실행
    - **`undo()`** : undo 버튼을 누를 때마다 지금까지 실행되었던 것들을 한개씩 pop해서 redo에 넣고 다시 그려주는 역할
    - **`redo()`** : redo 버튼을 누를 때 마다 redo 메모리에서 한개씩 pop해서 메모리에 넣고 다시 그려주는 역할
    - **`addCanvas()`** : new canvas 버튼을 누를 때 마다 새로운 Canvas 생성 및 Canvas group에 넣어주는 역할
    - **`setEraser()`** : eraser 버튼을 눌렀을 때 버튼 세팅
    - **`setText()`** : new text 버튼을 눌렀을 때 버튼 세팅하고 TextBoard 생성 및 Canvas group에 넣어주는 역할
    - **`setInit()`** : clear 버튼을 눌렀을 때 버튼 세팅 및 캔버스 초기화
    - **`setDraw()`** : draw 버튼을 눌렀을 때 각각의 맞는 도형이 그려지도록 세팅
- **`CanvasGroup class`** : 생성된 Canvas들과 TextBoard들을 모아두는 곳
- **`Canvas class`** : 그림을 그리기위한 Canvas
    - **`Canvas()`** : MyMouseListener 클래스를 Canvas에 추가
    - **`MyMouseListener를 class`** : 마우스가 눌렸을 때와 드레그 되었을 때, 놓였을 때로 나누어 MouseListener를 설정
        - **`paintComponent()`** : 실제로 Canvas에 그림이 그려지도록 Graphics를 사용해서 그림을 그리는 역할
- **`TextBoard class`** : 텍스트 모드에서 글을 쓰기위한 TextBoard
    - **`TextBoard()`** : 글을 쓸 수 있는 TextArea 설정
- **`Sketch class`** : 스케치를 위해 스케치의 시작점과 끝점을 저장하는 클래스
- **`Memory class`** : redo, undo를 위해 지금까지 그렸던 도형들을 저장하는 클래스
- **`ColorFrame class`** : 스케치나 도형을 그릴 때 색을 선택할 수 있도록 해주는 클래스
    - **`ColorFrame()`** : ChangeListener를 추가
    - **`stateChanged()`** : 색이 바뀔 때 마다 해당 색으로 지정
- **`CheckFrame class`** : Delete 버튼을 눌렀을 때 정말로 삭제할지 묻는 창
    - **`CheckFrame()`** : 정말로 삭제할지 묻는 라벨과 ActionListener를 추가한 yes, no 버튼 추가
    - **`actionPerformed()`** : yes 버튼 - Canvas 삭제 및 모든 메모리를 비워주고 창을 삭제,  
    no 버튼 - 해당 CheckFrame을 닫아주는 행동을 실행
- **`Stroke class`** : 라인의 굵기를 설정하는 클래스
    - **`Stroke()`** : ChangeListener를 추가
    - **`stateChanged()`** : 굵기가 바뀔 때마다 해당 굵기로 지정
- **`Clear class`** : 창을 초기화 시킬 때에 캔버스 화면에 맞는 하연 사각형 객체를 만들어주는 class

UML Diagram을 보면 알겠지만, 주요 클래스와 함수들만 설명했다.  
혹시 코드를 보고 궁금한 점이나 문의할 내용이 있으면 댓글로 남겨주세요!
<br/><br/><br/>

## 6. GitHub 및 프로젝트 보고서
제 코드는 아래 GitHub에서 확인 가능합니다 :)  
<https://github.com/0pencoding/JavaCamp-Round2-DrawBoard>

또한 위 코드 설명보다 더 자세한 설명이나 실행 결과가 필요하다면 아래 링크에서 보고서를 다운받을 수 있습니다 :)  
<https://drive.google.com/file/d/15mE3ce3AQZ2JYinjSA9cl54PlF53mcJc/view?usp=sharing>
<br/><br/><br/>

<!-- ## [[Round 3] 데이터 베이스 구현 ➜ ](abc)
{: style="text-align: right;"}
<br/> -->