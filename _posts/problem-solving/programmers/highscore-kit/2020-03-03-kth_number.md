---
title: "프로그래머스 고득점 Kit : K번째 수"
date: 2020-03-03
author: YuJin Kim
categories: [Problem Solving, Programmers, Highscore Kit]
tags: [programmers, highscore kit, level1, algorithm, sorting, c++, javascript]
sitemap:
  changefreq: daily
---

본 문제를 푸는 데에 큰 어려움은 없었지만 vector를 사용하는 데에 있어서 조금 공부가 필요했다. 아직까지 문제가 많이 어렵지는 않아서 난이도에 있어서나 문제를 푸는 시간에 있어서 그렇게 오래 걸리지는 않지만 C++을 잘 몰라 찾고 공부하는 데에 시간 소요가 있는 것 같다.  
<br/>
<br/>

## 1. 문제

배열 array의 i번째 숫자부터 j번째 숫자까지 자르고 정렬했을 때, k번째에 있는 수를 구하려 합니다.  
예를 들어 array가 [1, 5, 2, 6, 3, 7, 4], i = 2, j = 5, k = 3이라면 array의 2번째부터 5번째까지 자르면 [5, 2, 6, 3]입니다.  
1에서 나온 배열을 정렬하면 [2, 3, 5, 6]입니다. 2에서 나온 배열의 3번째 숫자는 5입니다.  
배열 array, [i, j, k]를 원소로 가진 2차원 배열 commands가 매개변수로 주어질 때, commands의 모든 원소에 대해 앞서 설명한 연산을 적용했을 때 나온 결과를 배열에 담아 return 하도록 solution 함수를 작성해주세요.

### 제한조건

- array의 길이는 1 이상 100 이하입니다.
- array의 각 원소는 1 이상 100 이하입니다.
- commands의 길이는 1 이상 50 이하입니다.
- commands의 각 원소는 길이가 3입니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. `commands` 벡터의 원소를 반복하며 각 원소의 `i`, `j`, `k` 값을 받는다.
2. 배열 `array`의 `i`부터 `j`까지 잘라 `cpVector` 벡터에 넣는다.
3. `sort()` 를 하용해서 `cpVector` 를 오름차순으로 정렬한다.
4. 정렬된 `cpVector`의 k번째 수를 `answer`에 넣는다.
5. `commands` 벡터의 반복이 끝나고 `answer`를 반환한다.  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <iostream>
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

vector<int> solution(vector<int> array, vector<vector<int>> commands) {
    vector<int> answer;

    for (int a = 0; a < commands.size(); a++) {
        vector<int> cpVector;
        int i = commands[a][0];
        int j = commands[a][1];
        int k = commands[a][2];

        cpVector.assign((array.begin()+i-1), (array.begin()+j));
        sort(cpVector.begin(), cpVector.end());
        answer.push_back(cpVector[k - 1]);
    }

    return answer;
}
```

<br/>

### [Javascript]

```javascript
function solution(array, commands) {
  var answer = [];

  commands.forEach(function (c) {
    answer.push(
      array.slice(c[0] - 1, c[1]).sort(function (a, b) {
        return a - b;
      })[c[2] - 1]
    );
  });

  return answer;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- `vector`에서 `copy`와 `assign`의 차이점
- 2차원 벡터 사용 방법
- sorting 방법
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- [STL] vector 복사 <https://terrorjang.tistory.com/85>
  > - vector를 전체 복사, 혹은 부분적으로 복사할 때 `copy`, `assign` 사용
  > - <span style="color: #c70000">`copy`와 `assign`의 차이점</span>  
  >   `copy`는 vector의 크기가 미리 할당 되어있어야하고, `assign`은 그러지 않아도 된다.
- [C++ STL] 동적 2차원 배열 사용법(vector) <https://sunnyholic.com/93>
  > - c++에서 2차원 vector에 접근할 때에는 c, java와 비슷하게 index로 접근
- [C++] sort algorithm 정리 및 예시 <https://blockdmask.tistory.com/178>

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
