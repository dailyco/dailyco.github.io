---
title: "프로그래머스 고득점 Kit :  N으로 표현"
date: 2020-08-07
author: YuJin Kim
categories: [Problem Solving, Programmers, Highscore Kit]
tags: [programmers, highscore kit, level3, algorithm, dynamic programming, c++]
sitemap:
  changefreq: daily
---

이 문제는 조금 많이 고민했고, 아직까지도 왜 DP 문제인지 잘 모르겠는 문제이다. 어떻게 어떻게 풀기는 했으나 진짜 효율성이 너무 똥망...(●´⌓`●) 아직 다른 사람 코드는 보지 않은 상태인데, 다른 사람 코드를 보면서 많이 공부해야하는 문제이다. 이 문제를 Dynamic Programming으로 푼 사람이 얼마나 될까..? 내가 푼 방법은 Dynamic Programming 이라기 보다는 Brute Force에 가까운 알고리즘 풀이 방식인 것 같다 ʘ̥﹏ʘ  
<br/>
<br/>

## 1. 문제

아래와 같이 5와 사칙연산만으로 12를 표현할 수 있습니다.

```
12 = 5 + 5 + (5 / 5) + (5 / 5)
12 = 55 / 5 + 5 / 5
12 = (55 + 5) / 5
```

5를 사용한 횟수는 각각 6,5,4 입니다. 그리고 이중 가장 작은 경우는 4입니다.  
이처럼 숫자 N과 number가 주어질 때, N과 사칙연산만 사용해서 표현 할 수 있는 방법 중 N 사용횟수의 최솟값을 return 하도록 solution 함수를 작성하세요.

### 제한조건

- N은 1 이상 9 이하입니다.
- number는 1 이상 32,000 이하입니다.
- 수식에는 괄호와 사칙연산만 가능하며 나누기 연산에서 나머지는 무시합니다.
- 최솟값이 8보다 크면 -1을 return 합니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. `N`을 key만큼 사용해서 만들 수 있는 숫자들을 value로 하는 맵 `c_values`를 생성한다.
2. `answer` 변수는 9로 초기화하여 해당 값보다 더 적은 숫자로 `number`를 만들 수 있으면 줄여주는 식으로 진행한다.
3. 처음에 `N`을 1개부터 8개까지 이어붙인 숫자를 생성하여 `c_values`에 넣어주고,  
   해당 숫자중 `number`와 일치하는 숫자가 있다면 `N`을 이어붙인 갯수를 반환시켜준다.
4. `N` 1개로 만들 수 있는 숫자들부터 7개로 만들 수 있는 숫자들끼리 반복해서 사칙 연산한 숫자가 `number`와 일치하는지 확인해 일치한다면 해당 숫자를 만든 `N`의 갯수를 확인해 `answer`보다 적은 갯수로 만들었다면 `answer`의 갯수를 해당 갯수로 할당한다. (사칙연산 중 나눗셈을 할 때에는 나누는 값이 0이 되어서는 안되므로 확인하는 과정을 추가한다)
5. 반복문이 끝나고 `answer`를 확인해 처음과 그대로인 9면 `number`와 일치하는 값을 못찾았다는 이야기이므로 -1을 반환하고 그렇지 않은 경우에는 `answer` 값을 반환한다.  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <vector>
#include <map>
#include <set>

using namespace std;

int solution(int N, int number) {
    map<int, set<int>> c_values;
    int answer = 9;

    int n = 0;
    for(int i = 1; i <= 8; i++) {
        n = n*10 + N;
        if(n == number) return i;
        c_values[i].insert(n);
    }

    for(int i = 1; i < 8; i++) {
        for(int j = 1; j < 8; j++) {
            if(i + j > 8) break;
            for(auto a = c_values[i].begin(); a != c_values[i].end(); a++) {
                for(auto b = c_values[j].begin(); b != c_values[j].end(); b++) {
                    if(*a + *b == number || *a - *b == number
                       || *a * *b == number || (*b != 0 && *a / *b == number)) {
                        if(i+j < answer) answer = i+j;
                    }
                    c_values[i+j].insert(*a + *b);
                    c_values[i+j].insert(*a - *b);
                    c_values[i+j].insert(*a * *b);
                    if(*b != 0) c_values[i+j].insert(*a / *b);
                }
            }
        }
    }

    return answer == 9? -1 : answer;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- 효율성이 O(n<sup>4</sup>)... 더 좋은 방법 생각해보기!
- DP로 푸는 방법 생각/찾아보기!
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- 없다 (´∩｡• ᵕ •｡∩`) ♡

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
