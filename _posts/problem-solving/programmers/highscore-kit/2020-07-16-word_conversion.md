---
title: "프로그래머스 고득점 Kit : 단어 변환"
date: 2020-07-16
author: YuJin Kim
categories: [Problem Solving, Programmers, Highscore Kit]
tags: [programmers, highscore kit, level3, algorithm, dfs/bfs, c++]
# sitemap:
#     changefreq: daily
---

어제 저녁에 문제를 읽고 자기 전에 어떻게 풀어야할지 생각하면서 알고리즘을 대충 세우고 오늘 일어나서 풀어보았는데 생각했던 알고리즘이 맞아서 빨리 풀 수 있었다. 다만, 문제에서 기본적으로 제공해주는 기본 테스트 케이스를 틀려서 살펴보았더니 테스트 케이스가 잘못된 것을 발견했다. 혹시나 나와 같이 뭐지? 싶었던 분은 그냥 테스트 케이스가 잘못된 것이니 무시하고 코드를 제출하여 채점해보길 바란다(\*´∇ ｀)ﾉ  
<br/>
<br/>

## 1. 문제

두 개의 단어 begin, target과 단어의 집합 words가 있습니다.  
아래와 같은 규칙을 이용하여 begin에서 target으로 변환하는 가장 짧은 변환 과정을 찾으려고 합니다.

```
1. 한 번에 한 개의 알파벳만 바꿀 수 있습니다.
2. words에 있는 단어로만 변환할 수 있습니다.
```

<br/>

예를 들어 begin이 hit, target가 cog, words가 [hot,dot,dog,lot,log,cog]라면 hit -> hot -> dot -> dog -> cog와 같이 4단계를 거쳐 변환할 수 있습니다.

두 개의 단어 begin, target과 단어의 집합 words가 매개변수로 주어질 때, 최소 몇 단계의 과정을 거쳐 begin을 target으로 변환할 수 있는지 return 하도록 solution 함수를 작성해주세요.

### 제한조건

- 각 단어는 알파벳 소문자로만 이루어져 있습니다.
- 각 단어의 길이는 3 이상 10 이하이며 모든 단어의 길이는 같습니다.
- words에는 3개 이상 50개 이하의 단어가 있으며 중복되는 단어는 없습니다.
- begin과 target은 같지 않습니다.
- 변환할 수 없는 경우에는 0를 return 합니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. 단어를 다른 단어로 변환할 수 있는지 확인하는 `canChange()` 함수를 생성한다.  
   (`canChange()` 함수는 두 단어를 비교해 서로 다른 알파벳이 한 개인지 확인하여 반환하는 함수)
2. 단어를 변환하며 최소 단계의 변환 횟수를 찾는 함수 `dfs()`를 생성한다.
3. `dfs()` 함수의 동작 방식은 다음과 같다.
4. 먼저 현재 단어를 `taget` 단어로 바꿀 수 있는지 확인해 바꿀 수 있다면 1을 반환한다.
5. `target` 단어로 바꿀 수 없으면, 현재 단어에서 변환할 수 있는 단어를 `words` 벡터 내에서 찾는다.
6. 벡터 내에 변환할 수 있는 단어가 있으면 또 다시 그 단어에서 변환 할 수 있는 다른 단어를 찾기 위해  
   벡터에서 해당 단어를 지우고 해당 단어를 `begin` 인자로, 해당 단어를 지운 벡터를 `words` 인자로하는 `dfs()` 함수에 재귀적으로 적용한다.
7. 반환되는 값이 현재 최소 변환 횟수 `answer`보다 작으면 해당 값으로 재설정해준다.
8. 반복이 끝나고, `words` 벡터에 변환할 수 있는 단어가 없으면 (`answer`가 그대로 50이면) 0을 반환한다.
9. 그렇지 않으면 최소 변환 횟수 `answer`를 반환한다.  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <string>
#include <vector>

using namespace std;

bool canChange(string prev, string next) {
    bool diff = false;

    for (int i = 0; i < prev.length(); i++) {
        if (prev[i] != next[i]) {
            if (diff) return false;
            else diff = true;
        }
    }

    return true;
}

int dfs(string begin, string target, vector<string> words) {
    if (canChange(begin, target)) return 1;

    int cAnswer, answer = 50;
    for (int i = 0; i < words.size(); i++) {
        if (canChange(begin, words[i])) {
            vector<string> words_cp = words;
            words_cp.erase(words_cp.begin() + i);
            cAnswer = dfs(words[i], target, words_cp);
            if (cAnswer != 0 && answer > cAnswer+1) answer = cAnswer+1;
        }
    }

    if (answer == 50) return 0;
    return answer;
}

int solution(string begin, string target, vector<string> words) {
    return dfs(begin, target, words);
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- 벡터 원소 삭제 방법
- 기본으로 제공해주는 테스트 케이스가 잘못되었다
- 빨리 해결해서 기분이 좋다
- 재귀 함수는 생각하기 힘들어...
- 열심히 공부해야지 (\*´◒`\*)
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- [C++ 공식문서] std:vector:erase <https://www.cplusplus.com/reference/vector/vector/erase/>
  > - 벡터의 원소 삭제는 `iterator`를 사용해서 삭제 가능, `vector.erase(iterator)` 형식으로 사용

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
