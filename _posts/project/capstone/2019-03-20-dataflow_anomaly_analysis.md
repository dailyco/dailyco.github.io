---
title: "데이터 흐름 이상 분석 (Dataflow Anomaly Analysis)"
date: 2019-03-20
author: YuJin Kim
categories: [Project, Capstone, PMD]
tags: [project, capstone, java, pmd, dataflow anomaly analysis, bug]
sitemap:
  changefreq: daily
---

[전 포스팅]({{site.url}}/posts/static_analysis) 중 PMD에 대해 간략히 설명했었다.  
이번 포스팅에서는 좀 더 나아가 PMD의 Dataflow Anomaly Analysis에 대해서 다뤄보려한다.  
<br/>
<br/>

## 1. Dataflow Anomaly Analysis

### 1) Dataflow Anomaly Analysis 란?

Dataflow Anomaly Analysis, 한국어로 번역하면 '데이터 흐름 이상 분석'이란 무엇인가?  
PMD에서 정의하는 Dataflow Anomaly Analysis의 정의는 다음과 같다.

> 어떠한 데이터에 정의 되어있는 변수의 흐름을 쫓아가면서 변수의 잘못된 정의나 참조를 분석  
> → 이로부터 다양한 문제(결함) 발견

간단히 말해서 변수의 흐름을 쫓으면서 변수가 잘못 정의 되지는 않았는지, 쓸데없는 정의가 존재하지는 않는지 등을 분석하고, 이로부터 결함을 발견하는 분석 방법이다.

### 2) data의 세 가지 상태

이러한 변수들은 각각 세 가지 상태를 가지는데, 그 종류는 아래와 같다.

- Defined (D) : 변수 x에 값이 할당 되면 변수 x가 defined 되었다고 한다.  
  ex) x = 5;

- Undefined (U) : 변수 x의 값이 삭제될 때 변수 x가 undefined 되었다고 한다.  
  ex) method의 지역 변수가 method가 종료되고 사라질 때

- Referenced (R) : 변수 x가 y의 값 혹은 조건문 등에 참조 될 때 referenced 되었다고 한다.  
  ex) y = x + 1; or if(x == 1)
  <br/>
  <br/>

## 2. Anomaly

PMD에서 변수의 흐름을 쫓으면서 분석을 할 때 각 변수(data)의 세 가지 상태 D, U, R에 대해 알아보았는데,  
이제 이 세가지 상태로 나타낸 Anomaly의 종류에 무엇이 있는지를 알아보자.

### 1) Anomaly 종류

Anomaly의 종류에는 UR, DU, DD Anomaly 세 종류가 있다.  
이 세 종류를 자세히 설명하기 전에, Anomaly의 개념이 조금 생소하실 수 있는 분을 위해 조금의 이해를 돕고자 살짝 언급하고 넘어가려한다.  
Anomaly는 한국어로 번역하면 '이상', '변칙'이라는 뜻을 가지는데, 여기에서 Anomaly는 단순히 '결함'으로 이해하면 좀 더 직관적이고 쉽게 다가오리라 생각한다.

- UR-Anomaly : UR이면 Undefined, Referenced이다.  
  이것만 보고 직관적으로 'UR-Anomaly가 뭐겠다!'하고 다가오시는 분들도 있으리라 생각한다.  
  UR-Anomaly(Undefined, Referenced-Anomaly)는 값이 존재하지 않는 변수를 참조했을 때 발생한다.  
  한 가지 상황을 예로 들어보면, y에 (x + 1)라는 값을 할당했는데 이전에 x에 값이 할당되어있지 않으면 이것은 잘못된 코드가 되고 PMD 이것을 UR-Anomaly로 판단하는 것이다.

- DU-Anomaly : DU면 Defined, Undefined이다.  
  이전의 설명을 보고난 후이기 때문에 더 쉽게 이해할 수 있을거라 생각한다.  
  DU-Anomaly(Defined, Undefined-Anomaly)는 변수를 사용하지 않고 바로 삭제할 때 발생한다.  
  예를 들면, 어떤 method에 지역 변수 x에 5라는 값을 할당하고 이 값을 사용하지 않고 method가 끝나버린 경우이다. 이러한 경우에 사용되지 않은 변수가 생성된 것이기 때문에 PMD는 이것을 DU-Anomaly로 판단한다.

- DD-Anomaly : DD면 Defined, Defined.  
  더 이상의 설명이 필요 없을거라 생각하지만, 설명해보자.  
  DD-Anomaly(Defined, Defined-Anomaly)는 변수에 값이 할당되고 다시 할당된 경우에 발생한다.  
  예를 들dj, x에 5라는 값을 할당하고 여기에 다시 바로 6이라는 값을 할당하면 5라는 값은 사용되지 않기 때문에 PMD에서는 이것을 결함으로 판단하고 DD-Anomaly로 구분한다.
  <br/>
  <br/>

### 2) Anomaly Example

이번 포스팅에서는 Data Flow Anomaly Analysis가 무엇인지에 대해 공부해 보았다.  
여기에서 마무리하기에는 조금 아쉽기 때문에, 간단한 예시를 보고 한 번 연습을 해보자.

```java
void MinMax(int min, int max) {
  int help;
  if (min > max) {
    max = help;
    max = min;
    help = min;
  }
  return;
}
```

<br/>
위의 자바 코드의 흐름을 처음부터 쭉 따라가보자.  
위 코드에서는 min, max, help 이렇게 세 개의 변수가 존재한다.  
처음 MinMax method를 시작하기 전에는 min, max, help 모두 Undefined 상태일 것이다.  
그리고 method가 시작하면 parameter에 들어온 값이 생성되면서 min, max가 Defined 될 것이다.  
그 다음 if문으로 가면 min과 max가 Referenced되고, if문 안에 들어갈 경우 max는 Defined, help는 Referenced가 될 것이다.
이런식으로 끝까지 쭉 가다보면 아래와 같이 흐름이 변할 것이다.
<br/>
```java
                                   // min, max, help => Undefined
void MinMax(int min, int max) {    // min, max => Defined
  int help;
  if (min > max) {                 // min, max => Referenced
    max = help;                    // max => Defined, help => Referenced
    max = min;                     // max => Defined, min => Referenced
    help = min;                    // help => Defined, min => Referenced
  }
  return;
}
                                   // min, max, help => Undefined
```
<br/>
이것을 표로 보기 좋게 나타내보면 아래와 같이 나타낼 수 있다.

| Variable\Path | start | in  | n1  | n2  | n3  | n4  | out | finish |
| :-----------: | :---: | :-: | :-: | :-: | :-: | :-: | :-: | :----: |
|      min      |   u   |  d  |  r  |     |  r  |  r  |  r  |   u    |
|      max      |   u   |  d  |  r  |  d  |  d  |     |  r  |   u    |
|     help      |   u   |     |     |  r  |     |  d  |     |   u    |

<br/>
위 표와 같이 나타내면 변수별 상태가 한 눈에 들어오기 때문에 변수 별로 어떤 Anomaly에 걸리는지 바로 확인할 수 있다.
그래서 확인해 보면, min변수와 help변수는 UR, DU, DD Anomaly 모두 해당 되지 않음을 알 수 있고, max 변수는 DD-Anomaly에 걸리는 것을 확인 할 수 있다.

자, 이렇게해서 간단한 예시까지 살펴봄으로써 우리는 PMD의 Data Flow Anomaly에 대해 완전히 이해하게 되었다.
사실 예제는 loop가 없는 간단한 예제였기 때문에 우리가 쉽게 생각할 수 있었지만 loop가 들어가게 되면 훨씬 복잡해지고 어려워진다.
혹시나 더 복잡하고 어려운 예제로 공부하고 싶은신 분이 있다면, 아래 Reference를 참고해서 공부해 나가길 바란다.
<br/>
<br/>

## 3. Reference

- 학습 자료 : <http://agde.informatik.uni-kl.de/teaching/sqs/ws2008/material/folien/SQA_07_DFA_4s.pdf>
