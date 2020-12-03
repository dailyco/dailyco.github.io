---
title: "프로그래머스 고득점 Kit : 숫자 야구"
date: 2020-03-11
author: YuJin Kim
categories: [Problem Solving, Programmers, Highscore Kit]
tags: [programmers, highscore kit, level2, algorithm, bruteforce, c++]
sitemap:
  changefreq: daily
---

본 문제는 문제를 읽자마자 바로 알고리즘이 떠올랐다. 하지만 정작 문제는 잘 해결되지 않았는데, 내가 문제를 자세하게 읽지 않아서 문제를 잘못 이해하고 있었다. 보통의 숫자야구를 생각해서 당연히 중복된 숫자가 가능하고, 0도 포함되어 있을거라 생각했으나 그게 아니었던 것이 복병이었던 것 같다. 역시 문제 속에 답이 있다고... •́︿•̀ 앞으로 문제를 꼼꼼히 읽는 습관을 들여야겠다.  
<br/>
<br/>

## 1. 문제

숫자 야구 게임이란 2명이 서로가 생각한 숫자를 맞추는 게임입니다. [게임해보기](https://scratch.mit.edu/projects/131352991/)  
각자 서로 다른 1~9까지 3자리 임의의 숫자를 정한 뒤 서로에게 3자리의 숫자를 불러서 결과를 확인합니다.  
그리고 그 결과를 토대로 상대가 정한 숫자를 예상한 뒤 맞힙니다.

```
- 숫자는 맞지만, 위치가 틀렸을 때는 볼
- 숫자와 위치가 모두 맞을 때는 스트라이크
- 숫자와 위치가 모두 틀렸을 때는 아웃
```

예를 들어, 아래의 경우가 있으면

```
A : 123
B : 1스트라이크 1볼.
A : 356
B : 1스트라이크 0볼.
A : 327
B : 2스트라이크 0볼.
A : 489
B : 0스트라이크 1볼.
```

이때 가능한 답은 324와 328 두 가지입니다.  
질문한 세 자리의 수, 스트라이크의 수, 볼의 수를 담은 2차원 배열 baseball이 매개변수로 주어질 때, 가능한 답의 개수를 return 하도록 solution 함수를 작성해주세요.

### 제한조건

- 질문의 수는 1 이상 100 이하의 자연수입니다.
- baseball의 각 행은 [세 자리의 수, 스트라이크의 수, 볼의 수] 를 담고 있습니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. 문제에서 서로 다른 1~9까지의 숫자라고 했기 때문에 반복문의 범위를 123에서 987으로 정해준다.
2. 각 숫자에 0이 포함되거나, 같은 숫자가 있을 경우는 건너뛴다.
3. 각 숫자를 `baseball`에 담긴 숫자들과 비교해서 `strike` 수와 `ball` 수를 구한다.
4. `baseball` 에 담긴 strike, ball 수와 `strike`, `ball` 이 모두 같으면 `answer`을 증가시킨다.
5. 반복문이 끝나면 `answer`를 반환한다.  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <string>
#include <vector>

using namespace std;

int solution(vector<vector<int>> baseball) {
    int answer = 0;

    for (int i = 123; i < 988; i++) {
        bool is_answer = true;
        string num = to_string(i);

        if (num.find('0') != -1) continue;
        if (num[0] == num[1] || num[0] == num[2] || num[1] == num[2]) continue;

        for (auto j : baseball) {
            string baseball_num = to_string(j[0]);
            int strike = 0, ball = 0;

            if (num[0] == baseball_num[0]) strike++;
            if (num[1] == baseball_num[1]) strike++;
            if (num[2] == baseball_num[2]) strike++;

            if (baseball_num.find(num[0]) != -1) ball++;
            if (baseball_num.find(num[1]) != -1) ball++;
            if (baseball_num.find(num[2]) != -1) ball++;

            ball -= strike;

            if (j[1] != strike || j[2] != ball)
                is_answer = false;
        }

        if (is_answer) answer++;
    }

    return answer;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- 문제를 잘 읽자!
- `string`에 접근하는 방법으로 `at()` 함수 말고 다른 방법도 있었네..
- `string.find()` 를 쓸 때 찾고자하는 문자열이 없을 때 `string::npos` 외에도 -1을 사용해서 비교 가능
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- [C++] string 클래스, 문자열에 대해서 (총정리) <https://blockdmask.tistory.com/338>
  > - string에서 char로 접근할 때 `at()` 함수로 접근하는 방법 외에도 index로 접근 가능
  > - 단, index로 접근했을 경우 형태는 char 형태로 다른 char과 비교할 때 '' 을 사용

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
