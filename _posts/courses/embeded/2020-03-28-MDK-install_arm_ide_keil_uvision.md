---
title: "MDK-ARM IDE Keil μVision 설치하기 (STM32F411RE)"
date: 2020-03-28
author: YuJin Kim
categories: [Courses, Embeded]
tags: [embeded, study, install, mdk-arm, stm32f411re]
sitemap:
  changefreq: daily
---

본 포스팅은 MDK-ARM IDE Keil μVision을 설치하는 방법을 이야기한다. 임베디드 과제를 하기 위해 세팅을 해야하는데 여기서부터 조금 헤메었던지라 혹시 나와 같은 사람이 있다면 도움이 되고자 포스팅을 작성한다. 처음에는 막막했는데 하나씩 찾아보면서 겨우겨우 설치했던터라 다른 사람들은 그렇지 않았으면 하는 마음에 자세히 적어보았다.  
<br/>
<br/>

## 1. MDK-ARM v5 설치하기

#### 1. MDK-ARM v5를 다운받기 위해 아래 홈페이지에 들어간다.

<https://www.keil.com/>  
<br/>

#### 2. 오른쪽 모서리의 'Downloads' 버튼을 클릭한다.

![step1](/assets/img/post/courses/embeded/1.png){:width="500px" class="normal"}  
<br/>

#### 3. Download Products에서 MDK-Arm을 선택한다.

![step2](/assets/img/post/courses/embeded/2.png){:width="500px" class="normal"}  
<br/>

#### 4. 정보를 입력해주고, 아래 'Submit' 버튼을 클릭한다. (본인은 정확한 정보 입력X)

![step3](/assets/img/post/courses/embeded/3.png){:width="500px" class="normal"}  
<br/>

#### 5. 현재의 가장 최신 버전인 MDK529.EXE를 다운받는다.

![step4](/assets/img/post/courses/embeded/4.png){:width="500px" class="normal"}  
<br/><br/><br/>

## 2. MDK-ARM v5 (MDK529) 설치

#### 1. 설치된 파일을 실행시킨다.

![step5](/assets/img/post/courses/embeded/5.png){:width="500px" class="normal"}  
<br/>

#### 2. 아래와 같은 창이 나오면 'Next'를 클릭한다.

![step6](/assets/img/post/courses/embeded/6.png){:width="500px" class="normal"}  
<br/>

#### 3. 라이센스에 동의를 하고, 다음으로 넘어간다.

![step7](/assets/img/post/courses/embeded/7.png){:width="500px" class="normal"}  
<br/>

#### 4. 자신이 저장하고싶은 위치를 설정해주고, 다음으로 넘어간다.

![step8](/assets/img/post/courses/embeded/8.png){:width="500px" class="normal"}  
<br/>

#### 5. 이름과 회사, 이메일 등의 정보(노란박스) 를 입력하고 넘어간다. (본인은 정확한 정보 입력X)

![step9](/assets/img/post/courses/embeded/9.png){:width="500px" class="normal"}  
<br/>

#### 6. 아래와 같이 설치 진행중인 창이 나오는데 설치될동안 기다린다.

![step10](/assets/img/post/courses/embeded/10.png){:width="500px" class="normal"}  
<br/>

#### 7. 설치가 끝나고나면 아래와 같은 창이 새롭게 뜨는데 설치해준다.

![step11](/assets/img/post/courses/embeded/11.png){:width="500px" class="normal"}  
<br/>

#### 8. 설치를 마치기위해 'Finish' 를 클릭한다.

![step12](/assets/img/post/courses/embeded/12.png){:width="500px" class="normal"}  
<br/><br/><br/>

## 3. [Optional] Pack Installer를 이용해서 STM32F411RE를 위한 Pack 설치

아래 과정은 선택사항이다.  
그때그때 자신이 필요한 pack을 설치해도되고, 프로젝트를 생성할 때마다 사용하는 pack을 선택해줄 수도 있다.  
<br/>

#### 1. 설치가 완료되고나면 아래와 같은창이 자동으로 켜지는데, 'OK'를 클릭한다.

![step13](/assets/img/post/courses/embeded/13.png){:width="500px" class="normal"}  
<br/>

#### 2. 사용하는 보드를 위한 팩을 설치해주기 위해서 먼저 자신의 보드를 찾는다.

Search 에 자신이 사용하는 보드의 이름을 검색한다.  
<br/>
![step14](/assets/img/post/courses/embeded/14.png){:width="500px" class="normal"}  
<br/>

#### 3. 사용하는 보드를 클릭해주면 오른쪽의 Packs (노란색) 부분이 해당 보드를 사용하기 위해 필요한 pack들을 보여준다.

![step15](/assets/img/post/courses/embeded/15.png){:width="500px" class="normal"}  
<br/>

#### 4. 필요한 pack들을 설치/업데이트 해준다.

![step16](/assets/img/post/courses/embeded/16.png){:width="500px" class="normal"}  
<br/>

#### 5. 중간에 아래와 같은 라이센스 동의를위한 창이 나올 수 있는데, 동의하고 넘어간다.

![step17](/assets/img/post/courses/embeded/17.png){:width="500px" class="normal"}  
<br/><br/><br/>

## 4. Reference

- Keil uVision5-ARM을 위한 컴파일러 <https://vo.la/CBX2>
