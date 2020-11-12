---
title: "프로그래머스 고득점 Kit : 등굣길"
date: 2020-08-07
author: YuJin Kim
categories: [Programmers, Highscore Kit]
tags: [programmers, highscore kit, level3, algorithm, dynamic programming, c++]
# sitemap:
#     changefreq: daily
---

이 문제는 예전에 남자친구가 나에게 냈었던 문제였기 때문에 알고리즘 자체는 그 때 풀었던대로 빠르게 세울 수 있었다. 그런데 빨리 풀겠다는 자만심 때문이었는지 알고리즘을 세우는 데에 있어서 조그만 실수를 한 부분 때문에 어디가 잘못되었는지 찾느라고 30분 정도를 소비한 것 같다. 이미 알고있는 문제라고, level3 문제 좀 푼다고 자만하면 안되는데 인간은 정말 끝없이 실수를 반복하는 것 같다 へ[ •́ ‸ •̀ ]ʋ  
<br/>
<br/>

## 1. 문제

계속되는 폭우로 일부 지역이 물에 잠겼습니다. 물에 잠기지 않은 지역을 통해 학교를 가려고 합니다.  
집에서 학교까지 가는 길은 m x n 크기의 격자모양으로 나타낼 수 있습니다.

아래 그림은 m = 4, n = 3 인 경우입니다.

![mn_board](https://grepp-programmers.s3.amazonaws.com/files/ybm/056f54e618/f167a3bc-e140-4fa8-a8f8-326a99e0f567.png){:width="300" class="normal"}

가장 왼쪽 위, 즉 집이 있는 곳의 좌표는 (1, 1)로 나타내고  
가장 오른쪽 아래, 즉 학교가 있는 곳의 좌표는 (m, n)으로 나타냅니다.

격자의 크기 m, n과 물이 잠긴 지역의 좌표를 담은 2차원 배열 puddles이 매개변수로 주어집니다.  
집에서 학교까지 갈 수 있는 최단경로의 개수를 1,000,000,007로 나눈 나머지를 return 하도록 solution 함수를 작성해주세요.

### 제한조건

- 격자의 크기 m, n은 1 이상 100 이하인 자연수입니다.
  - m과 n이 모두 1인 경우는 입력으로 주어지지 않습니다.
- 물에 잠긴 지역은 0개 이상 10개 이하입니다.
- 집과 학교가 물에 잠긴 경우는 입력으로 주어지지 않습니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. (m+1)×(n+1) 크기의 이차원 벡터의 값을 모두 -1로 초기화한 mn 변수를 생성한다.  
   (해당 변수는 각 지역까지 최단경로로 갈 수 있는 경우의 수를 나타낼 변수이다)
2. 이차원 벡터의 [1][1] 좌표는 1로, [0][x] 좌표와 [x][0] 좌표는 모두 0으로 초기화한다.
3. puddle 이차원 벡터를 사용해서 물에 잠긴 지역은 어차피 해당 지역으로 갈 수 없으니 0을 할당한다.
4. 이차원 벡터 mn을 돌면서 아직 최단경로로 갈 수 있는 경우의 수를 구하지 않았다면(해당 지역 값이 -1이라면)  
   해당 지역의 왼쪽과 위쪽 지역에 최단경로로 갈 수 있는 경우의 수를 더해 1,000,000,007로 나눈 나머지로 나타낸다.  
   (최단 경로로 해당 지역에 도착하기 위해서는 오른쪽과 아래로만 이동해야한다(물론 예외 케이스가 있긴하다)  
   따라서 왼쪽에서 해당 지역에 오는 경우와 위쪽에서 해당 지역에 오는 경우를 합하여 경우의 수를 구해주고,  
   문제 상에서 최단경로의 개수를 1,000,000,007로 나눈 나머지를 구하라고 했으므로  
   계산 중에 overflow가 일어나는 것을 고려해 해당 값으로 나눈 나머지를 넣어준다.)
5. 반복문이 끝나면 (m, n) 좌표의 값을 반환한다.  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <vector>

using namespace std;

int solution(int m, int n, vector<vector<int>> puddles) {
    vector<vector<int>> mn(n+1, vector<int>(m+1, -1));

    mn[1][1] = 1;
    for(int i = 1; i < m+1; i++) mn[0][i] = 0;
    for(int i = 1; i < n+1; i++) mn[i][0] = 0;
    for(auto puddle : puddles) mn[puddle[1]][puddle[0]] = 0;

    for(int i = 1; i < n+1; i++)
        for(int j = 1; j < m+1; j++)
            if(mn[i][j] == -1)
                mn[i][j] = (mn[i-1][j] + mn[i][j-1]) % 1000000007;

    return mn[n][m];
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- 2차원 벡터 초기화 방법
- 알고리즘을 세우고 꼼꼼히 확인하기!
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- 2 차원 std :: vector 초기화  
  <https://www.it-swarm.dev/ko/c%2B%2B/2-%EC%B0%A8%EC%9B%90-std-vector-%EC%B4%88%EA%B8%B0%ED%99%94/1041384922/>
  > - 2차원 벡터를 생성과 동시에 초기화를 시킬 때는 `vector<vector<data_type>> var_name(row_number, vector<data_type>(col_number, initialize_value))` 를 사용

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
