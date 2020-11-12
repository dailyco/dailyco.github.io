---
title: "프로그래머스 고득점 Kit : 모의고사"
date: 2020-03-04
author: YuJin Kim
categories: [Programmers, Highscore Kit]
tags: [programmers, highscore kit, level1, algorithm, bruteforce, c++]
# sitemap:
#     changefreq: daily
---

본 문제를 풀면서 가장 뿌듯했던 것은 각 수포자가 찍는 방식을 미리 array로 만들어둔것이다. 다른 사람이 생각할 때 '그게 왜?'라고 생각할 수 있지만, 평소에 내가 생각하고 있던 것이 아니라 문제를 풀면서 퍼뜩하고 생각나서 더 그랬던 것 같다.  
<br/>
<br/>

## 1. 문제

수포자는 수학을 포기한 사람의 준말입니다.  
수포자 삼인방은 모의고사에 수학 문제를 전부 찍으려 합니다.  
수포자는 1번 문제부터 마지막 문제까지 다음과 같이 찍습니다.

- 1번 수포자가 찍는 방식: 1, 2, 3, 4, 5, 1, 2, 3, 4, 5, ...
- 2번 수포자가 찍는 방식: 2, 1, 2, 3, 2, 4, 2, 5, 2, 1, 2, 3, 2, 4, 2, 5, ...
- 3번 수포자가 찍는 방식: 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, 3, 3, 1, 1, 2, 2, 4, 4, 5, 5, ...

1번 문제부터 마지막 문제까지의 정답이 순서대로 들은 배열 answers가 주어졌을 때, 가장 많은 문제를 맞힌 사람이 누구인지 배열에 담아 return 하도록 solution 함수를 작성해주세요.

### 제한조건

- 시험은 최대 10,000 문제로 구성되어있습니다.
- 문제의 정답은 1, 2, 3, 4, 5중 하나입니다.
- 가장 높은 점수를 받은 사람이 여럿일 경우, return하는 값을 오름차순 정렬해주세요.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. answer 벡터에 1,2,3을 미리 초기화 시키고, 각 수포자가 찍는 방식을 벡터로 생성한다.
2. 각 수포자가 찍는 방식의 벡터와 답인 answers 벡터를 비교하여 각 수포자가 맞은 문제수를 센다.
3. 각 수포자가 맞은 문제수가 가장 크지 않으면, answer 벡터에서 삭제한다.
4. answer 벡터를 반환한다.  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <string>
#include <vector>

using namespace std;

vector<int> solution(vector<int> answers) {
    vector<int> answer{1, 2, 3};
    vector<int> first{1, 2, 3, 4, 5};
    vector<int> second{2, 1, 2, 3, 2, 4, 2, 5};
    vector<int> third{3, 3, 1, 1, 2, 2, 4, 4, 5, 5};

    int one = 0, two = 0, three = 0;
    for(int i = 0; i < answers.size(); i++) {
        if (first[i%first.size()] == answers[i]) one++;
        if (second[i%second.size()] == answers[i]) two++;
        if (third[i%third.size()] == answers[i]) three++;
    }

    if (one < two || one < three) answer.erase(answer.begin());
    if (two < one || two < three) answer.erase(answer.end() - 2);
    if (three < one || three < two) answer.erase(answer.end() - 1);

    return answer;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- 각 수포자가찍는 방식을 어떻게 나타낼지가 포인트 (처음에 알고리즘적으로 접근 but...)
- 문제를 맞힌 갯수가 가장 큰 수포자들을 골라내는 부분도 생각해볼 필요가 있다
- 다른 사람은 max를 찾아 max와 같은지 한 번더 비교해주는 방법
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- [C++ 공식문서] std:vector:erase <http://www.cplusplus.com/reference/vector/vector/erase/>

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
