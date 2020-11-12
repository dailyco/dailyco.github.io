---
title: "프로그래머스 고득점 Kit : 네트워크"
date: 2020-07-15
author: YuJin Kim
categories: [Programmers, Highscore Kit]
tags: [programmers, highscore kit, level3, algorithm, dfs/bfs, c++]
# sitemap:
#     changefreq: daily
---

이 문제는 풀릴듯 풀리지 않아서 시간을 조금 썼던 문제이다. 완성된 코드도 썩 마음에 들지는 않지만, 다음에 시간을 들여 좀 더 코드를 다듬어 봐야겠다. 프로그래머스 고득점 Kit 문제를 풀기 전에는 DFS/BFS 문제에 대해서 풀기도 전에 겁을 먹게 되었는데, 이렇게 level3 문제를 한 개씩 풀어가면서 확실히 풀 수 있다는 자신감은 생기는 것 같다. 이 마음이 자만심이 되기까지는 한 끝 차이이기 때문에 항상 조심하면서 더욱 성장해가는 내가 되었으면 좋겠다 !(•̀ᴗ•́)و ̑̑  
<br/>
<br/>

## 1. 문제

네트워크란 컴퓨터 상호 간에 정보를 교환할 수 있도록 연결된 형태를 의미합니다.  
예를 들어, 컴퓨터 A와 컴퓨터 B가 직접적으로 연결되어있고, 컴퓨터 B와 컴퓨터 C가 직접적으로 연결되어 있을 때  
컴퓨터 A와 컴퓨터 C도 간접적으로 연결되어 정보를 교환할 수 있습니다.  
따라서 컴퓨터 A, B, C는 모두 같은 네트워크 상에 있다고 할 수 있습니다.

컴퓨터의 개수 n, 연결에 대한 정보가 담긴 2차원 배열 computers가 매개변수로 주어질 때,  
네트워크의 개수를 return 하도록 solution 함수를 작성하시오.

### 제한조건

- 컴퓨터의 개수 n은 1 이상 200 이하인 자연수입니다.
- 각 컴퓨터는 0부터 n-1인 정수로 표현합니다.
- i번 컴퓨터와 j번 컴퓨터가 연결되어 있으면 computers[i][j]를 1로 표현합니다.
- computer[i][i]는 항상 1입니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. 글로벌 변수 network_board를 생성한다.
2. 인자로 받은 computers 2차원 벡터를 글로벌 변수 network_board에 할당한다.  
   (파라미터로 계속해서 넘겨주면 메모리 손실이 클 것 같아서)
3. 네트워크 수를 나타내는 answer 벡터를 0으로 초기화시켜 생성하고, 2차원 벡터의 크기만큼 다음을 반복한다.
4. 2차원 벡터의 해당 값(컴퓨터 연결상태)이 1이면 answer를 증가시키고(네트워크 한 개가 생성되는 것),  
   dfs() 함수를 사용해서 연결된 컴퓨터들의 값을 전부 0으로 바꿔준다.
5. dfs() 함수가 어떻게 작용하는지를 보면, 해당 컴퓨터 연결상태는 0으로 바꿔주고,  
   연결된 컴퓨터를 기준으로 0부터 탐색하면서 또 다른 컴퓨터랑 연결되어있으면 dfs() 함수를 재귀적으로 사용한다.
6. 반복이 끝나면, answer 값을 반환한다.  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <string>
#include <vector>

using namespace std;
vector<vector<int>> network_board;

void dfs(int i, int j, int n) {
    network_board[i][j] = 0;
    for (int k = 0; k < n; k++)
        if (network_board[j][k] == 1) dfs(j, k, n);
}

int solution(int n, vector<vector<int>> computers) {
    network_board = computers;
    int answer = 0;

    for(int i = 0; i < n; i++)
        for(int j = 0; j < n; j++)
            if (network_board[i][j] == 1) {
                answer++;
                dfs(i, j, n);
            }

    return answer;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- 좀 더 효율성 좋게 바꿀 수 있을 것 같다!
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- 없다 \|•˙-˙•)و✧

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
