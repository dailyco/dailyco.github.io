---
title: "프로그래머스 고득점 Kit : 구명보트"
date: 2020-03-22
author: YuJin Kim
categories: [Programmers, Highscore Kit]
tags: [programmers, highscore kit, level2, algorithm, greedy, c++]
# sitemap:
#     changefreq: daily
---

본 문제는 굉장히 빨리 풀었지만 효율성 때문에 엄청 헤멨다. 효율성 때문에 코드를 엎고, 질문하기를 찾아보면서 어떻게 해야 더 좋은 코드를 짤 수 있는지 굉장히 고민을 많이 했던 문제였다. 정확도는 다 맞았는데 효율성 때문에 통과 못하니 너무 답답하고 스트레스를 받았는데, 알고리즘을 공부하는 이유가 결국 효율성 좋게 문제를 해결하기 위함이므로 좋은 코드를 짤 수 있도록 계속해서 고민하고 노력해야겠다고 생각했다.  
<br/>
<br/>

## 1. 문제

무인도에 갇힌 사람들을 구명보트를 이용하여 구출하려고 합니다.  
구명보트는 작아서 한 번에 최대 2명씩 밖에 탈 수 없고, 무게 제한도 있습니다.

예를 들어, 사람들의 몸무게가 [70kg, 50kg, 80kg, 50kg]이고 구명보트의 무게 제한이 100kg이라면 2번째 사람과 4번째 사람은 같이 탈 수 있지만 1번째 사람과 3번째 사람의 무게의 합은 150kg이므로 구명보트의 무게 제한을 초과하여 같이 탈 수 없습니다.

구명보트를 최대한 적게 사용하여 모든 사람을 구출하려고 합니다.

사람들의 몸무게를 담은 배열 people과 구명보트의 무게 제한 limit가 매개변수로 주어질 때, 모든 사람을 구출하기 위해 필요한 구명보트 개수의 최솟값을 return 하도록 solution 함수를 작성해주세요.

### 제한조건

- 무인도에 갇힌 사람은 1명 이상 50,000명 이하입니다.
- 각 사람의 몸무게는 40kg 이상 240kg 이하입니다.
- 구명보트의 무게 제한은 40kg 이상 240kg 이하입니다.
- 구명보트의 무게 제한은 항상 사람들의 몸무게 중 최댓값보다 크게 주어지므로 사람들을 구출할 수 없는 경우는 없습니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. 사람들의 몸무게를 담은 people 벡터를 오름차 순으로 정렬한다.
2. j는 왼쪽(처음)부터, i는 오른쪽(끝)에서 시작한다.
3. 몇 명이 보트에 타든, 보트 한 개가 필요할 것이기 때문에 answer를 증가시킨다.
4. i와 j가 같으면 모든 사람이 보트에 탔다는 말이므로 반복문을 나간다(break).
5. people의 j와 i를 더했을 때 limit을 넘지않으면 j를 증가시켜 다음으로 무게가 적은 사람을 가리키게 한다.  
   (limit을 넘지 않으면 두 명을 한 보트에 태울 수 있는 것이므로 i도 감소시켜야하지만, i는 for문에서 계속해서 감소되기 때문에 건들지 않는다)
6. 반복문이 끝나면, answer를 반환한다.  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <vector>
#include <algorithm>

using namespace std;

int solution(vector<int> people, int limit) {
    int answer = 0;
    int j = 0;

    sort(people.begin(), people.end());

    for (int i = people.size() - 1; i >= j; i--) {
        answer++;
        if (i == j) break;
        if (people[i] + people[j] <= limit) j++;
    }

    return answer;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- 처음에 복잡도 O(n^2)로 풀었는데 생각해보니까 O(n)으로 풀 수 있었어..
- vector.pop_back() 함수나 vector.erase() 함수 사용하면 효율성 통과 못함
- 효율성이 진짜 중요하구나
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- vector::push_back() and vector::pop_back() in C++ STL  
   <https://www.geeksforgeeks.org/vectorpush_back-vectorpop_back-c-stl/>
  > - 사용하진 않았지만 vector에서 마지막 원소를 더하고 빼는 함수 `vector.push_back()`, `vector.pop_back()` 사용

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
