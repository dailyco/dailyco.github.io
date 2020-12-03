---
title: "프로그래머스 고득점 Kit : 기능개발"
date: 2020-03-17
author: YuJin Kim
categories: [Problem Solving, Programmers, Highscore Kit]
tags: [programmers, highscore kit, level2, algorithm, stack-queue, c++]
sitemap:
  changefreq: daily
---

이 문제도 '[[스택/큐] 탑]({{site.url}}/posts/top)' 문제랑 비슷하게 level2 인것 치고는 쉬운 문제라는 생각이 들었다. 딱 문제를 읽자마자 '어, 이거 금방 풀 수 있을 것 같은데?' 하는 생각이 떠올랐고, 예상대로 문제는 무척 빨리 풀렸다. 비록 while문을 두개로 중첩해서 사용해서 효율성은 떨어지지만... 그리고 풀고나서 다른 사람 풀이를 보다가 내가 전에 이 문제와 비슷한 문제를 더 효율성 좋게 푼적이 있었던 것이 생각나서 내 자신이 정말 바보라고 생각했었다...ㅠㅠ  
<br/>
<br/>

## 1. 문제

프로그래머스 팀에서는 기능 개선 작업을 수행 중입니다.  
각 기능은 진도가 100%일 때 서비스에 반영할 수 있습니다.

또, 각 기능의 개발속도는 모두 다르기 때문에 뒤에 있는 기능이 앞에 있는 기능보다 먼저 개발될 수 있고, 이때 뒤에 있는 기능은 앞에 있는 기능이 배포될 때 함께 배포됩니다.

먼저 배포되어야 하는 순서대로 작업의 진도가 적힌 정수 배열 progresses와 각 작업의 개발 속도가 적힌 정수 배열 speeds가 주어질 때 각 배포마다 몇 개의 기능이 배포되는지를 return 하도록 solution 함수를 완성하세요.

### 제한조건

- 작업의 개수(progresses, speeds배열의 길이)는 100개 이하입니다.
- 작업 진도는 100 미만의 자연수입니다.
- 작업 속도는 100 이하의 자연수입니다.
- 배포는 하루에 한 번만 할 수 있으며, 하루의 끝에 이루어진다고 가정합니다. 예를 들어 진도율이 95%인 작업의 개발 속도가 하루에 4%라면 배포는 2일 뒤에 이루어집니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. `speeds`의 크기와 `progresses`의 크기는 동일하니 하나를 선택해서 `size`가 0이 될 때까지 다음을 반복한다.  
   (`speeds`와 `progresses`의 각 원소가 작업이 끝나면 지워주는 식으로 진행했기 때문에)
2. 해당 `progress`를 수행하는데 걸리는 시간을 구해 `day`에 넣고, 해당 `progress`와 `speed`는 지운다.  
   (`progress`를 수행하는데 걸리는 시간 = (100-`progress`)/`speed`를 올림한 값)
3. 다음 `progress`부터 시작해서 `progress`를 수행하는데 걸리는 시간이 이전 시간(`day`)보다 클 때까지  
   `progress`와 `speed`를 지우고, `count`는 증가시키는 것을 반복한다.
4. `answer`에 `count`를 push한다.
5. `speeds` 혹은 `progresses`의 사이즈가 0이 되어서 반복문이 끝나면, `answer`를 반환한다.  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <vector>
#include <cmath>

using namespace std;

vector<int> solution(vector<int> progresses, vector<int> speeds) {
    vector<int> answer;

    while(speeds.size()) {
        int count = 1;
        int day = ceil((100 - progresses[0])/(double)speeds[0]);

        progresses.erase(progresses.begin());
        speeds.erase(speeds.begin());

        while(speeds.size()
              && day >= ceil((100 - progresses[0])/(double)speeds[0])) {
            progresses.erase(progresses.begin());
            speeds.erase(speeds.begin());
            count++;
        }

        answer.push_back(count);
    }

    return answer;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- 올림을 위해서는 어떤 함수를 써야하지?
- 명시적 형변환 어떻게 사용하는지 python이랑 헷갈린다..
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- [C언어/C++] 올림, 내림, 반올림 (floor, ceil) 함수 <https://blockdmask.tistory.com/112>
  > - 올림을 위해서는 `ceil()` 함수, 내림을 위해서는 `floor()` 함수, 반올림을 위해서는 해당 숫자에 0.5를 더하고 `floor()` 함수 적용!
  > - `ceil()` 함수와 `floor()` 함수를 사용하기 위해서는 `#include <cmath>`
- [C++ 정리] 명시적 형변환 & 묵시적 형변환 <http://myblog.opendocs.co.kr/archives/1249>
  > - 명시적 형변환은 `(자료형)변수` 로 사용

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
