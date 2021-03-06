---
title: "2019 KAKAO BLIND RECRUITMENT : 실패율"
date: 2020-07-03
author: YuJin Kim
categories: [Problem Solving, Programmers, Kakao]
tags: [programmers, level1, algorithm, sorting, c++]
sitemap:
  changefreq: daily
---

해당 문제는 level1인 만큼 쉬운편에 속했다. 다만 내가 생각하지 못한 부분이 있어서, 디버깅하는 데에 시간이 좀 걸렸다ㅠㅠ 카카오 문제를 풀면서 느끼는 건데, 카카오 코딩 테스트 문제의 질이 정말 좋은 것 같다. 그냥 우리가 흔히 아는 자료구조를 선택해서 바로 코드를 작성하는 문제들이 아니라 자료 구조를 어떤 것을 사용할지 선택하고 그 자료구조를 사용해서 어떻게 풀지 제대로 알고리즘을 세워 문제를 풀어야한다는 느낌이랄까...? 정확하게 설명하기는 어려운데 코딩 테스트 연습을 하는데에 정말 많은 도움이 된다. (_•̀ᴗ•́_)و ̑̑  
<br/>
<br/>

## 1. 문제

![kakao_game](https://grepp-programmers.s3.amazonaws.com/files/production/bde471d8ac/48ddf1cc-c4ea-499d-b431-9727ee799191.png){: width="300" class="normal"}

슈퍼 게임 개발자 오렐리는 큰 고민에 빠졌다.  
그녀가 만든 프랜즈 오천성이 대성공을 거뒀지만, 요즘 신규 사용자의 수가 급감한 것이다.  
원인은 신규 사용자와 기존 사용자 사이에 스테이지 차이가 너무 큰 것이 문제였다.

이 문제를 어떻게 할까 고민 한 그녀는 동적으로 게임 시간을 늘려서 난이도를 조절하기로 했다.  
역시 슈퍼 개발자라 대부분의 로직은 쉽게 구현했지만, 실패율을 구하는 부분에서 위기에 빠지고 말았다.  
오렐리를 위해 실패율을 구하는 코드를 완성하라.

- 실패율은 다음과 같이 정의한다.
  - 스테이지에 도달했으나 아직 클리어하지 못한 플레이어의 수 / 스테이지에 도달한 플레이어 수

전체 스테이지의 개수 N, 게임을 이용하는 사용자가 현재 멈춰있는 스테이지의 번호가 담긴 배열 stages가 매개변수로 주어질 때, 실패율이 높은 스테이지부터 내림차순으로 스테이지의 번호가 담겨있는 배열을 return 하도록 solution 함수를 완성하라.

### 제한조건

- 스테이지의 개수 N은 1 이상 500 이하의 자연수이다.
- stages의 길이는 1 이상 200,000 이하이다.
- stages에는 1 이상 N + 1 이하의 자연수가 담겨있다.
  - 각 자연수는 사용자가 현재 도전 중인 스테이지의 번호를 나타낸다.
  - 단, N + 1 은 마지막 스테이지(N 번째 스테이지) 까지 클리어 한 사용자를 나타낸다.
- 만약 실패율이 같은 스테이지가 있다면 작은 번호의 스테이지가 먼저 오도록 하면 된다.
- 스테이지에 도달한 유저가 없는 경우 해당 스테이지의 실패율은 0 으로 정의한다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. 스테이지-해당 스테이지의 실패율 쌍을 원소로하는 벡터 `stage_frate`와 `answer` 벡터를 생성한다.
2. 스테이지를 나타내는 `i`를 1부터 N까지 반복하면서 해당 스테이지에 도달한 플레이어 수 `reach_player` 와,  
   스테이지에 도달했으나 아직 클리어하지 못한 플레이어 수 `nclear_player` 를 구한다.
3. 구한 `reach_player`, `nclear_player` 값을 나눠 실패율을 구하고 해당 스테이지-실패율 `stage_frate` 쌍을 벡터에 push한다. (`reach_player`가 0인 경우 분모가 0이 되고 문제의 제한조건에 의해 실패율은 0으로 정의한다)
4. 반복문이 끝나면 `stage_frate` 함수를 내가 정의한 `compare` 함수에 따라 정렬한다.  
   (`compare` 함수는 실패율을 기준으로 실패율 높은 순서대로, 실패율이 같을 경우 스테이지가 낮은 순서대로 정렬)
5. 정렬된 `stage_frate` 벡터를 반복하며 스테이지만 `answer` 벡터에 push한다.
6. `stage_frate` 벡터의 반복이 끝나면, `answer` 를 반환한다.  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

bool compare(pair<int, double> a, pair<int, double> b) {
    if (a.second == b.second) return a.first < b.first;
    else return a.second > b.second;
}

vector<int> solution(int N, vector<int> stages) {
    vector<pair<int, double>> stage_frate;
    vector<int> answer;

    for(int i = 1; i <= N; i++) {
        double reach_player = 0;
        double nclear_player = 0;
        for(int j = 0; j < stages.size(); j++) {
            if(i <= stages[j]) reach_player++;
            if(i == stages[j]) nclear_player++;
        }

        stage_frate.push_back(
            make_pair(i, reach_player == 0? 0.0 : nclear_player/reach_player));
    }
    sort(stage_frate.begin(), stage_frate.end(), compare);

    for(auto s_f_pair : stage_frate)
        answer.push_back(s_f_pair.first);

    return answer;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- 벡터 정렬할 때, 내가 직접 생성한 함수 기준으로 정렬하는데, 정렬 기준이 두 개인 경우 유의하기
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- [C++] sort algorithm 정리 및 예시 <https://blockdmask.tistory.com/178>
  > - 사용자 정의 함수를 기준으로 정렬할 경우 `sort()`의 세번째 파라미터로 해당 변수를 넣어주고, 정렬 기준이 두 개인 경우 사용자 정의 함수에 1순위 정렬 기준이 같을 경우 2순위 정렬 기준으로 정렬한다는 내용을 담아서 사용

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
