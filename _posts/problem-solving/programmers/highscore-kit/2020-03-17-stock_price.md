---
title: "프로그래머스 고득점 Kit : 주식가격"
date: 2020-03-17
author: YuJin Kim
categories: [Problem Solving, Programmers, Highscore Kit]
tags: [programmers, highscore kit, level2, algorithm, stack-queue, c++]
sitemap:
  changefreq: daily
---

본 문제는 처음에 문제를 잘 이해하지 못해서 함께 문제를 푸는 언니에게 물어보았다. 처음에는 문제를 잘못 이해했다가 '이거 조금 이상한 것 같은데?' 하는 생각이 들었다가 언니의 설명을 듣고 이해가 되었고, 문제를 이해한 뒤에는 문제를 푸는 데에는 그렇게 오래 걸리지 않았다. 루프를 두 번 돌기 때문에 효율성이 좋다고 말할 수는 없지만 다른 사람들도 비슷하게 푼 것 같아 완전 비효율적으로 문제를 푼건 아니라는 생각이 들었다.  
<br/>
<br/>

## 1. 문제

초 단위로 기록된 주식가격이 담긴 배열 prices가 매개변수로 주어질 때,  
가격이 떨어지지 않은 기간은 몇 초인지를 return 하도록 solution 함수를 완성하세요.

### 제한조건

- prices의 각 가격은 1 이상 10,000 이하인 자연수입니다.
- prices의 길이는 2 이상 100,000 이하입니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. `prices` 벡터의 원소를 반복하면서 각 원소를 `p`로 받고 `count`는 0부터 시작한다.
2. 현재 원소의 다음 원소부터 시작해서 다음 원소가 현재 원소 `p`보다 크거나 작은(가격이 떨어지지 않은) 동안 `count`를 증가시킨다.
3. 가격이 떨어지지 않은 기간을 나타내는 `count` 값을 `answer`에 push한다.
4. `prices` 벡터의 반복이 끝나면 `answer`를 반환한다.  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <string>
#include <vector>

using namespace std;

vector<int> solution(vector<int> prices) {
    vector<int> answer;

    for (int i = 0; i < prices.size(); i++) {
        int p = prices[i];
        int count = 0;

        for (int j = i; p <= prices[j] && j < prices.size() - 1; j++) count ++;

        answer.push_back(count);
    }

    return answer;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- `prices.size()` - 1 은 가격이 떨어지지 않은 기간이기 때문에 `prices` 마지막 원소는 고려해주지 않은 것!
- 처음에 문제가 제대로 이해가 안돼서 당황쓰.. 막상 풀고나니 쉬운 문제!
- 그러나 여전히 스택/큐는 사용하지 않았다
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- 없다! 점점 스스로 해결해 가는 것 같아 뿌듯 :)

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
