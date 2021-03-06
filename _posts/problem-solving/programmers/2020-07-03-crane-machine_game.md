---
title: "2019 카카오 개발자 겨울 인턴십 : 크레인 인형뽑기 게임"
date: 2020-07-03
author: YuJin Kim
categories: [Problem Solving, Programmers, Kakao]
tags: [programmers, level1, algorithm, stack-queue, c++]
sitemap:
  changefreq: daily
---

이 문제는 해결하는데 시간이 오래 걸리지도 않았고, 디버깅 없이 바로 해결되었다. 난이도가 level인 만큼 쉬웠던 것 같다. 다만 문제의 지문이 조금 길어서 읽는데 시간 소모가 조금 있었다. 이 문제를 풀고, 다른 사람 풀이를 봤는데 굳이 나 처럼 스택 생성해 사용하지 않고도 그냥 매개변수로 주어지는 2차원 벡터 형태 그대로 사용해서 문제를 해결할 수 있다는 사실을 알고 내가 너무 알고리즘 "문제 풀이 = 자료구조 선택"에 집중해 있었다는 생각이 들었다. 문제를 풀 때, 편협한 생각에서 벗어나서 좀 더 자유롭게 사고할 수 있었으면 좋겠다!  
<br/>
<br/>

## 1. 문제

게임개발자인 죠르디는 크레인 인형뽑기 기계를 모바일 게임으로 만들려고 합니다.  
죠르디는 게임의 재미를 높이기 위해 화면 구성과 규칙을 다음과 같이 게임 로직에 반영하려고 합니다.

![kakao_crane_game1](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/69f1cd36-09f4-4435-8363-b71a650f7448/crane_game_101.png){: width="300" class="normal"}

게임 화면은 1 x 1 크기의 칸들로 이루어진 N x N 크기의 정사각 격자이며 위쪽에는 크레인이 있고 오른쪽에는 바구니가 있습니다. (위 그림은 5 x 5 크기의 예시입니다). 각 격자 칸에는 다양한 인형이 들어 있으며 인형이 없는 칸은 빈칸입니다.  
모든 인형은 1 x 1 크기의 격자 한 칸을 차지하며 격자의 가장 아래 칸부터 차곡차곡 쌓여 있습니다.  
게임 사용자는 크레인을 좌우로 움직여서 멈춘 위치에서 가장 위에 있는 인형을 집어 올릴 수 있습니다.  
집어 올린 인형은 바구니에 쌓이게 되는 데, 이때 바구니의 가장 아래 칸부터 인형이 순서대로 쌓이게 됩니다.  
다음 그림은 [1번, 5번, 3번] 위치에서 순서대로 인형을 집어 올려 바구니에 담은 모습입니다.  
<br/>

![kakao_crane_game2](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/638e2162-b1e4-4bbb-b0d7-62d31e97d75c/crane_game_102.png){: width="300" class="normal"}

만약 같은 모양의 인형 두 개가 바구니에 연속해서 쌓이게 되면 두 인형은 터뜨려지면서 바구니에서 사라지게 됩니다.  
위 상태에서 이어서 [5번] 위치에서 인형을 집어 바구니에 쌓으면 같은 모양 인형 두 개가 없어집니다.  
<br/>

![kakao_crane_game3](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/8569d736-091e-4771-b2d3-7a6e95a20c22/crane_game_103.gif){: width="300" class="normal"}

크레인 작동 시 인형이 집어지지 않는 경우는 없으나 만약 인형이 없는 곳에서 크레인을 작동시키는 경우에는 아무런 일도 일어나지 않습니다. 또한 바구니는 모든 인형이 들어갈 수 있을 만큼 충분히 크다고 가정합니다. (그림에서는 화면표시 제약으로 5칸만으로 표현하였음)

게임 화면의 격자의 상태가 담긴 2차원 배열 board와 인형을 집기 위해 크레인을 작동시킨 위치가 담긴 배열 moves가 매개변수로 주어질 때, 크레인을 모두 작동시킨 후 터트려져 사라진 인형의 개수를 return 하도록 solution 함수를 완성해주세요.

### 제한조건

- board 배열은 2차원 배열로 크기는 5 x 5 이상 30 x 30 이하입니다.
- board의 각 칸에는 0 이상 100 이하인 정수가 담겨있습니다.
  - 0은 빈 칸을 나타냅니다.
  - 1 ~ 100의 각 숫자는 각기 다른 인형의 모양을 의미하며 같은 숫자는 같은 모양의 인형을 나타냅니다.
- moves 배열의 크기는 1 이상 1,000 이하입니다.
- moves 배열 각 원소들의 값은 1 이상이며 board 배열의 가로 크기 이하인 자연수입니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. `board` 벡터를 세로 기준으로 스택 형태로 재초기화할 `board_stack`과 `answer`를 생성한다.
2. `board`의 가로, 세로 크기로 N을 초기화한다.
3. `board` 를 세로 기준의 스택 형태로 재초기화한다.  
   (`board` 의 마지막 원소부터 원소가 0이 아닌경우에 스택에 push)
4. `basket` 스택을 생성하고, 좀 더 수월한 비교를 위해 -1을 push 해준다.
5. `moves` 벡터를 반복하며 각 원소에 대해 다음을 반복한다.
6. `board_stack` 에 해당 스택이 비었으면 다음으로 넘어간다.
7. `board_stack` 에 해당 스택에 값이 있으면 맨 위의 값과 `basket` 의 맨 위의 값을 비교해 같으면 `answer`를 2 증가시키고, `board_stack` 의 해당 스택과 `basket` 을 pop 해준다. (같은 모양 인형 두 개가 없어진 경우)
8. `board_stack` 에 해당 스택에 값이 있고, 맨 위의 값과 `basket` 의 맨 위의 값을 비교해 다르면 `basket` 에 해당 인형을 push하고 `board_stack`의 해당 스택에서는 pop 해준다. (`board` 에서 `basket` 에 인형을 옮긴 경우)
9. `moves` 의 반복이 끝나면, `answer`를 반환한다.  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <string>
#include <vector>
#include <stack>

using namespace std;

int solution(vector<vector<int>> board, vector<int> moves) {
    vector<stack<int>> board_stack;
    int N = board.size();
    int answer = 0;

    for(int i = 0; i < N; i++) {
        stack<int> s;
        for(int j = N - 1; j >= 0; j--)
            if(board[j][i] != 0) s.push(board[j][i]);
        board_stack.push_back(s);
    }

    stack<int> basket;
    basket.push(-1);
    for(int idx : moves) {
        idx--;
        if(board_stack[idx].empty()) continue;
        if(board_stack[idx].top() == basket.top()) {
            answer += 2;
            board_stack[idx].pop();
            basket.pop();
        } else {
            basket.push(board_stack[idx].top());
            board_stack[idx].pop();
        }
    }

    return answer;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- 스택이 비었는지 확인하는 방법
- 마지막에 `basket` 에 -1 넣지 않고 for문을 반복하면서 `basket`이 비었는지 확인하며 진행하면 코드가 더 깔끔!
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- [C++ 공식문서] std:stack:empty <https://www.cplusplus.com/reference/stack/stack/empty/>
  > - 스택이 비었는지 확인하는 방법은 `stack.empty()`를 사용

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
