---
layout: post
title: "[Compiler] Compiler 공부 첫번째 : Compiler란 무엇인가?"
date: 2020-04-22
categories: Compiler
tags: compiler study
sitemap:
    changefreq: daily
---

오늘부터 컴파일러 공부를 해보려한다. 현재 컴파일러 수업을 듣고 있는데, 시험기간이기도하고 공부를 하려고보니 블로그에 정리하면서 공부하면 좋을 것 같다는 생각이 들었기 때문이다. 원래는 실습만 올리려고했는데 이렇게 공부하면 더 자세히 잘 이해할 수 있을 것 같아 한 번 도전해본다. 작심삼일이 되지 않기를... 화이팅!  
<br/>

<br/>
### ⏰ㅤCompiler 공부 1

공부 양을 어떻게 나눌까 고민하다가 지금 실제로 수업을 듣고 있으니까 수업에 맞춰서 공부하면 더욱 좋을 것 같아 수업에 맞추기위해 앞 부분을 빠르게 진행하기로 했다.  
아, 미리 말해두지만 나는 compiler에 대해 잘 아는 전문가가 아니고 그저 공부하는 대학생일 뿐이기 때문에 아래 내용들이 정확하지 않을 수 있다.  
또한 공부한 것을 내가 이해한대로 정리하려고 작성하는 것이기 때문에 정확한 단어가 아닐수 있다는 것을 미리 알린다.  
그리고 모든 내용은 저자 Kenneth C.Louden의 Compiler Construction: Principles and Practice 책을 기반으로 한다.
<br/><br/><br/>

## 1. Compiler란 무엇인가
<q> Compilers are computer programs that translate one language to another. </q>

책에 따르면 컴파일러는 위와 같이 정의된다.  
즉, input으로 받은 source language을 사용해서 동일한 기능을 수행하는 target language로 변환시킨다.  
이를 그림으로 표현하면 아래와 같이 표현할 수 있다.  
<br/>

![compiler](/assets/img/post/Compiler/1.png){:width="600px"}  
<br/>
이 말만 듣고는 조금 추상적으로 들릴 수 있는데, 실질적인 예를 들어서 이야기하면  
일반적으로 input으로 들어가는 source language는 C, C++과 같은 high-level language이고,  
그에 따른 target language는 object code(= machine code) or assembly code 이다.  
<br/><br/><br/>

## 2. Compiler와 관련있는 프로그램
### a. Interpreters
ㅤㅤ인터프리터는 컴파일러와 같이 언어를 변환시킨다는 점에서 동일하다. 컴파일러와 다른점은 컴파일러는 source program을 완전히 변환시켜 object code를 만든 후에 실행시키는 반면에, 인터프리터는 source program을 즉시 실행시킨다. 원칙상으로는 모든 언어가 인터프리터와 컴파일러를 모두 사용할 수 있지만, 언어마다 다른 특성을 가지고 있기 때문에 컴파일러를 사용하면 좋은 것이 있고, 인터프리터를 사용하면 좋은 것이 있다. 예로는 BASIC 언어는 인터프리터를 사용하는 것이, LISP 언어는 컴파일러를 사용하는 것이 일반적이다. 이에 대해서 좀 더 자세하게 공부하고 싶으면, language translation에 대해서 좀 더 알아보는 것이 좋을 것 같다. (language translation: compile, interprete, hybrid)  
<br/>

### b. Assemblers
ㅤㅤAssembler는 assembly language를 변환하는 것이다. Assemly language를 무엇으로 변환시키냐? Object code로 변환시킨다. 그러니까 인풋으로 받은 source program을 컴파일러 내에서  assembler language로 변환되고 이것이 다시 assembler를 통해 object code로 변환되어 나오는 것이다. 여기서 참고해야할 점은 모든 컴파일러가 꼭 이런 형태를 띄는 것이 아니라, object code로 assembly language를 만들기도 하기 때문에, 이런 경우는 assembler를 사용해서 다시 object code로 변환시켜 주어야 한다.  
<br/>

### c. Linkers
ㅤㅤLinker는 다른 object file들을 실행할 수 있는 하나의 파일로 모아주는 역할을 한다. 또한 linker는 object program과 standard library function 혹은 os에서 제공하는 자원인 메모리나 인풋 아웃풋 기기들과 연결하는 역할도 한다. 사실 이 부분은 os에서 더 자세하게 다루고있기 때문에 이 부분에 대해서 더 깊게 공부하고 싶으면 os를 공부해보는걸 추천한다.  
<br/>

### d. Loaders
ㅤㅤLoader는 relocatable address를 다룬다. Relocatable address는 compiler나 assembler linker에서 생성하는 코드로, 아직 완벽하지 않은 실행 준비가 덜 된 코드들을 말한다. 메모리에서 코드의 위치가 언제든 변할 수 있기 때문에 relocatable address라고 표현하는 것 같다. 그래서 로더를 사용하면 실행 코드가 좀 더 flexible하다고 한다. 그리고 로더는 별개로 사용하지 않고 링커와 함께 이어져 사용되거나 운영 환경에서 실행된다.  
<br/>

### e. Preprocessors
ㅤㅤPreprocessor는 컴파일러 전에 실행되는 별개의 프로그램으로, 주석이나 다른 파일들을 삭제하고 macro substitution을 수행한다. macro subsititution은 반복되는 짧은 문장 등을 변환시켜주는 것을 의미한다.  
<br/>

### f. Editors
ㅤㅤ컴파일러와 관련된 프로그램으로 Editor도 있다는 것만 알고 넘어가면 될 것 같다. 특별하게 알아야할 내용은 없어보여서 넘어간다. 혹시 이 부분에 대해서 더 자세하게 알고 싶으면 저자 Kenneth C.Louden의 Compiler Construction: Principles and Practice 책을 읽어보시길!  
<br/>

### g. Debuggers
ㅤㅤDebugger는 컴파일러 IDE에 패키징되어있는 경우가 많으며 실행 에러는 찾는데 사용된다. 디버거는 프로그램이 실행되는 과정을 tracking 하며 정보를 저장하고, 자신이 원하는 지점에 break point를 걸어 해당 지점에서의 정보를 얻을 수 있다. 하지만 실제로 디버거의 기능을 수행하도록 하는 것은 무척 어렵고, 특히 컴파일러에서 object code를 최적화 시킬때는 scope 문제 때문에 더 어려워진다.
<br/>

### h. Profilers
ㅤㅤProfiler는 object program이 실행될 때 각 절차의 시행 시간을 퍼센트로한 값이나 각 절차의 시행 횟수와 같은 통계를 수집한다. 이러한 통계값은 개발자가 추후에 실행 속도나 효율성 측면에서 향상시키는 데에 무척 도움이 된다.  
<br/>

### i. Project Managers
ㅤㅤ요즘 소프트웨어 프로젝트가 무척 크기 때문에 한 개발자가 모두 개발하는 것이 아닌 여러명의 개발자가 개발한다. 그리고 이런 경우에 각각 다른 사람들이 작업한 파일을 관리하는 것이 중요한데 이 일을 해주는 것이 Project manager의 역할이다. 두개의 유명한 프로젝트 매니저로 Unix에서의 sccs(source code control system), rcs(rivision control system)이 있다. 나는 설명을 읽고 개인적으로 Github이 생각났는데 흔히 우리가 사용하는 Github의 기능들을 생각하면 될 것 같다.  
<br/><br/><br/>

## 3. Compiler 의 변환 과정
![compiler](/assets/img/post/Compiler/2.png){:width="450px"}  
<br/>

컴파일러의 변환 과정을 개략도로 나타내면 위와 같다.  
한 단계씩 자세히 살펴보면,
* Scanner: Source program으로부터 코드를 읽어들여 lexical analysis 과정을 수행시켜 token들을 생성
* Parser: Scanner에서 받은 token들을 syntax analysis를 통해 parse tree 또는 syntax tree 생성
* Semantic Analyzer: ㅡ
* Source code Optimizer: 
* Code Generator: 
* Target code Optimizer: 

그리고 컴파일러 변환 과정에서 사용되는 주 데이터 구조는 아래와 같다.  
* Token: 
* Syntax Tree: 
* Symbol Table: 
* Literal Table: 
* Intermediate Code: 
* Temporary File: 
<br/><br/><br/>

## 4. Compiler 의 변환 과정 자세히
위에서 설명한 각 변환 과정들은 정말 말그대로 간단하게 한줄로만 설명한 것이다.  
실제로 한 단계씩 보면 각 단계마다 정말 많은 내용을 담고 있기 때문에 따로 나누어 정리하려한다.  

1. Scanner
    * [Scanner란 무엇인가?]()
    * [Scanner, Java로 구현해보기]()


<br/><br/><br/>

## 5. 참고
* Book: Compiler Construction: Principles and Practice (Kenneth C.Louden)
<br/><br/><br/>

<!-- ## [[Compiler] Compiler 공부 두번째 :  ➜ ](https://0pencoding.github.io/)
{: style="text-align: right;"}
<br/> -->