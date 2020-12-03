---
title: "Java GUI 프로젝트 도전기 : 이미지 프로세싱 포토샵 만들기"
date: 2020-03-14
author: YuJin Kim
categories: [Project, Java Camp]
tags: [project, java camp, java, gui, image processing]
sitemap:
  changefreq: daily
---

### ⏰ 기간 4일 ⏰

벌써 프로젝트의 반이 끝났다는 사실이 놀랍다. 내 생각에는 항상 이맘때 즈음이 가장 힘든 시기인 것 같다. 중간쯤 왔을 때 지금까지 해왔던 과정을 한 번 더 해야한다는 마음과 그냥 포기하고 싶은 마음의 갈등 속에 있을 때, 더욱 힘내서 다음 단계로 나아갔으면 좋겠다. 네번째 프로젝트는 이미지 프로세싱이다. 이미지를 가지고 조작하는 것이다. 프로젝트를 진행하지 않는 사람들에게는 나의 코드와 설명이 유용한 정보가 되길 바란다 :)  
<br/>
<br/>

## 1. 기능

- 이미지 파일 읽어오기, 이미지 흑백 반전, 이미지 엣지추출, 대비, 밝기 조절, 이미지 합성, 돋보기  
  中 최소 4가지 이상 필수 선택
- 이외에 자유롭게 자신이 선보이고 싶은 기능, 있으면 좋겠다 싶은 기능 추가
- 주의할 점 : OpenCV를 사용하면 안된다
  <br/><br/><br/>

## 2. 시작!

이미지 프로세싱을 처음해본 나에게는 재밌기도 했지만 뭔가 수학적으로 이미지를 재해석하는 과정에 있어서 조금 힘들었다. Reference를 제공하긴 하지만, 필요한 개념과 자료는 더 많이 필요할 거라 생각한다.  
Reference 아래로는 나의 결과물과 설명이 이어진다. 꼭 4일 후에 본 프로젝트를 마무리하고 확인하길 바란다.  
그냥 내 코드와 결과물을 보고 공부한다면 그것도 물론 공부가 되겠지만 자신이 직접 찾아가며 한 공부보다는 훨씬 못할 것이다. 이전에도 말했듯이 그 당시에는 몰랐지만 지금보면 내 코드도 잘 짜여진 코드는 아님을 참고해주었으면 좋겠다.

### Reference

- [자바 이미지 사이즈 비율 변경 (java image resize)](https://huskdoll.tistory.com/826)
- [[Java] grayscale로 이미지 저장하기](https://blog.leocat.kr/notes/2016/01/12/java-save-to-grayscale)
  <br/><br/><br/>

## 3. 결과물

![imageprocessing](/assets/img/post/project/java-camp/imageprocessing.png){:width="600px" class="normal"}

### 구현 기능

- 이미지 파일 읽어오기, 이미지 흑백 반전, 밝기 조절, 돋보기, 이미지 엣지추출
- 사진의 해당 마우스 위치의 RGB 값 표기
- undo, redo 기능
- 이미지 모자이크
- 이미지 초기화

### 보완 해야할 부분

- 사진을 불러오지 않았을 때 RGB값이 없어 오류가 나는 문제
- 사진을 불러왔을 때 이미지의 크기를 화면에 맞게 조절
- 모자이크 효과 후에 다른 효과를 줄 때 모자이크 효과 사라지는 문제
- 다른 효과를 클릭 했을 때 밝기 조절 바가 있다면 없애주기 및 밝기 조절 효과 종료
  <br/><br/><br/>

## 4. 세부 기능 캡쳐

ㅤ![imageprocessing_detail](</assets/img/post/project/java-camp/imageprocessing_detail(1).png>){:width="500px" class="normal"}  
<br/>
ㅤ![imageprocessing_detail](</assets/img/post/project/java-camp/imageprocessing_detail(2).png>){:width="700px" class="normal"}  
<br/>
ㅤ![imageprocessing_detail](</assets/img/post/project/java-camp/imageprocessing_detail(3).png>){:width="700px" class="normal"}
<br/><br/><br/>

## 5. 코드 세부 설명

![imageprocessing_uml](/assets/img/post/project/java-camp/imageprocessing_uml.gif){:width="800px" class="normal"}

위 사진은 내 코드를 UML Diagram으로 나타낸 것이다.  
확실히 프로젝트를 진행하면서 어떻게 객체 지향적으로 코드를 짜야하는지를 배워가는 것 같다.

코드를 세부적으로 설명하면 아래와 같다.

- **`Main class`** : ImageProcessing의 큰 틀이 되는 Frame으로 각 버튼들을 눌렀을 때 행동 제어
  - **`Main()`** : Frame 세팅 및 각 버튼들과 메뉴바 설정
  - **`actionPerformed()`** : 버튼들을 눌렀을 때 각 버튼에 맞는 행동을 하는 함수 실행
  - **`stateChanged()`** : 밝기 조절과 관련해서 state가 바뀔 때 마다 맞는 행동을 제어
  - **`나머지 함수들`** : 버튼에 맞는 행동들을 하는 함수들
- **`ImagePanel class`** : 이미지를 돋보기 시키기 위한 클래스로 돋보기 시킨 이미지 자체를 그리는 역할
- **`Magnifier class`** : 이미지를 감싸는 틀인 돋보기 자체를 그리는 역할
- **`MenuBar class`** : 파일을 불러오고 저장하는 역할, 메뉴바 구성
- **`ButtonsPanel class`** : 이미지를 조작하기위한 버튼들 구성
- **`Memory class`** : undo, redo를 위한 메모리 구성
- **`BrightSlider class`** : 이미지의 밝기를 조절하는 slider로 밝기 값 자체를 구성

UML Diagram을 보면 알겠지만, 주요 클래스와 함수들만 설명했다.  
혹시 코드를 보고 궁금한 점이나 문의할 내용이 있으면 댓글로 남겨주세요!
<br/><br/><br/>

## 6. GitHub 및 프로젝트 보고서

- GitHub: <https://github.com/{{site.social.name}}/java-camp/tree/main/image-processing>
- Report: <https://drive.google.com/file/d/1UzaaQ9yTvtG25G2l08lBilVSrMqooShG/view?usp=sharing>  
  보고서는 더 자세한 설명이 필요한 경우 확인해주세요, 무단 배포는 허용하지 않습니다!
