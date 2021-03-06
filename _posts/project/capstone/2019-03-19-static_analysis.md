---
title: "정적 분석 도구 (Static Analysis Tool)"
date: 2019-03-19
author: YuJin Kim
categories: [Project, Capstone, PMD]
tags: [project, capstone, java, pmd, static analysis tool, bug]
sitemap:
  changefreq: daily
---

정적 분석 기법(Static Analysis)이란 무엇인가?  
이번 포스팅에서는 정적 분석 기법이 무엇이고, 정적 분석 중 하나인 PMD에 대해 알아보자.  
<br/>
<br/>

## 1. 정적 분석

### 1) 정적 분석 기법(Static Analysis)이란?

> 소스 코드의 실행 없이, 코드의 의미를 분석해 결함을 찾아내는 코드 분석 기법

정의만 읽었을 때 코드의 의미를 분석한다는 것이 좀처럼 와닿지 않을 수 있는데,  
이에 대한 설명은 정적 분석 도구의 전체적인 분석 과정을 통해 이야기하겠다.

### 2) 정적 분석 도구의 분석 과정

![static_analysis](/assets/img/post/project/capstone/static_analysis.png){:width="250"}
_그림1. 정적 분석 과정_

<!-- <figure style="width: 300px" class="align-center">
  <img src="{{ '/images/posts/static_analysis.png' }}" alt="">
  <figcaption>그림1. 정적 분석 과정</figcaption>
</figure> -->

- Program Model Constructor : 소스 코드를 분석해 중간코드로 변환
- Program Path Analyzer : 중간코드를 분석해 실제 실행 경로를 추적하면서 결함 리스트 작성

그림이 복잡해 보일 수 있는데, 막상 보면 매우 쉬운 그림이다.  
소스 코드를 정적 분석 도구에 입력하면 Program Model Constructor가 코드를 중간코드로 변환한다.  
중간코드에는 변수의 범위나 실행 경로를 추적할 수 있는 정보들이 담겨져 있으며, 이 코드를 Program Path Analyzer가 분석해 실제 실행되는 경로를 추적하면서 결함으로 의심되는 항목을 찾아 리스트를 작성하고, 그 리스트를 사용자에게 보여줌으로써 사용자가 결함 리스트를 검토하고 실제 결함을 찾도록 도와준다.
<br/>
<br/>

## 2. 정적 분석 기법을 사용하는 이유

왜 우리는 위와 같은 정적 분석 기법을 사용해야할까?  
사람들이 정적 분석 기법을 사용하는 이유를 소프트웨어의 개발 과정과 더불어 살펴보자.

### 1) 소프트웨어의 개발 과정

![static_analysis](/assets/img/post/project/capstone/software_develop.png){:width="500"}
_그림2. 소프트웨어 개발 과정_

소프트웨어 개발 과정을 5단계로 나누면 위 그림과 같으며, 정적 분석 기법은 세 번째 코딩 단계에서 사용된다.
코딩 단계는 일반적인 코딩 과정과 정적 분석 도구를 사용한 코딩 과정으로 나누어 볼 수 있는데, 그 내용은 아래 사진과 같다.

![static_analysis](/assets/img/post/project/capstone/coding.png){:width="400"}
_그림3. 일반적인 코딩 과정(좌), 정적 분석 도구를 사용한 코딩과정(우)_

일반적인 코딩 과정은 코드를 작성하고, Compile error를 발견했을때 코드를 수정하는 과정을 반복하다가 compile error가 더이상 발견되지 않으면 check in 한다. 정적 분석 도구를 사용하면 여기에 한 가지 과정이 추가 되는데, Compile error가 더이상 발견되지 않더라도 정적 분석 도구를 사용해서 결함이 있는지 확인한 후 결함이 존재하면 수정하는 과정을 반복한다.
<br/>

### 2) 정적 분석 기법을 사용했을 때 좋은 점

그러면 정적 분석 도구를 사용해서 결함이 있는지 확인하는 과정이 추가되었을 때 무엇이 좋을까?  
예를 들어 개발자가 작성한 코드에 버퍼 오버런이 존재한다고 할 때, 일반적인 코딩 과정을 따르면 테스팅 단계에서 오류를 발견할 것이다. 하지만 정적 분석 도구를 사용하면 코드 작성 후에 정적 분석 도구를 사용함으로써 버퍼 오버런을 발견할 수 있고 이 때 수정이 가능해진다.  
따라서 수정된 부분이 다른 코드에 미치는 영향을 최소화하기 때문에 테스팅 단계에서의 부담을 줄일 수 있고 높은 품질의 소프트웨어 출시가 가능해지게 되는 것이다.
<br/>
<br/>

## 3. 정적 분석 도구 : PMD

자, 본격적으로 정적 분석 도구를 알아보자.  
앞서 말했듯이, 정적 분석 도구는 소스 코드의 실행 없이 코드의 의미를 분석해 결함을 찾아내는 역할을 한다.  
정적 분석 도구에는 PMD, Sparrow, SonarQube 등 여러가지 종류가 있지만, 필자는 PMD라는 오픈소스를 대상으로 프로젝트를 진행할 예정이기 때문에 PMD에 대해서만 간략히 설명하겠다.

### 1) PMD

![static_analysis](/assets/img/post/project/capstone/pmd.png){:width="200"}
_그림4. PMD 공식 로고_

- PMD 공식 사이트 : <https://pmd.github.io/>
- PMD GitHub site : <https://github.com/pmd/pmd>
- PMD Download : [Click to download PMD](https://github.com/pmd/pmd/releases/download/pmd_releases%2F6.12.0/pmd-bin-6.12.0.zip)
  {: style="text-align: center;"}

PMD는 일련의 규칙에 근거하여 사용되지 않는 변수, 빈 catch 블록, 불필요한 개체 생성 등과 같은 일반적인 프로그램의 결함을 찾아내며 JAVA, JAVAScript, Visual force, PLSQL 등에 적용 가능하다.
<br/>
<br/>

## 4. 연구의 목표, 기대 효과

> **목표**  
> 오픈소스 정적 분석 도구 PMD의 규칙을 개선함으로써 False Positive를 줄이고,  
> 소프트웨어 결함 검출과 유지, 보수에 소요되는 비용의 효과적 절감을 기대한다.

PMD가 정적 분석 도구이고 어떤 결함들을 찾아내는지 대충 알겠는데 필자가 하려고 하는 것이 무엇이냐?  
필자는 위에서 계속해서 정적 분석 도구가 주는 이점에 대해 설명했었다.  
하지만 이 정적 분석 도구가 좋은점만 있느냐에 대한 질문에 쉽게 그렇다고 대답할 수 없다.

말했다시피, 정적 분석 도구는 코드의 결함을 탐지해 사용자에게 리스트를 보여준다.  
그러나 리스트가 모두 진짜 결함이라고 단정지을 수 없기 때문에 사용자는 리스트를 보고 확인 과정을 거치는데, 이 때에 정적 분석 도구가 결함이 아닌 것을 결함으로 탐지해 리스트에 보여주면 오탐지 결과 즉, False positive를 발생 시킨 것이다.
이 False positive(이하 FP)는 정적 분석 도구에서 꽤 흔히 일어나는 일이며, 개발자를 혼란스럽게 만든다.
이런 문제를 해결하기 위해서는 정적 분석 도구에서 결함이라고 예측하는 잣대인 일련의 규칙을 개발자들 개인이 사용하기 편리하게 직접 수정하는 과정이 필요한데, 이 과정은 개발자들에게 있어서 매우 귀찮은 과정일 뿐 아니라 차라리 정적 분석 도구를 사용하지 않는 것이 시간 대비 더 나은 효율성을 가질 수 있다.

따라서 필자는 정적분석 도구가 오탐지를 최소화하도록 규칙을 수정함으로써 FP를 줄이고 정적 분석 도구가 더욱 나은 결함 예측이 가능하도록 하려한다.
규칙 수정이 정확하게 이루어진 분석 도구를 사용하면, 소프트웨어 결함 검출과 유지 및 보수에 소요되는 비용을 효과적으로 절감할 수 있을 것이라는 효과를 기대한다.
<br/>
<br/>

## 5. Reference

- 논문: [KCSE 2019] 버그 검출 규칙 개선을 위한 코드 문맥 수집 방법에 대한 연구
- Guest Article: [SW개발 과정에서 효과적인 정적 분석 기법 적용방법](http://index-of.co.uk/Reverse-Engineering/SW2.pdf)
