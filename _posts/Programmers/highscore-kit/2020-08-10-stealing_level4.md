---
title: "프로그래머스 고득점 Kit : 도둑질"
date: 2020-08-10
author: YuJin Kim
categories: [Programmers, Highscore Kit]
tags: [programmers, highscore kit, level4, algorithm, dynamic programming, c++]
# sitemap:
#     changefreq: daily
---

이 문제는 첫 level4 문제이자, 처음으로(?) 내가 푼 문제가 아니다. 처음이 아닐지도 모르지만, 체감상... 여튼, 생각할 시간이 충분하지 못해서 이 문제를 푼 친구에게 알고리즘을 듣고 해당 알고리즘대로 내가 다시 풀어보았던 문제이다. 좀 더 생각해보면서 충분히 고민하고 싶었는데 이건 내가 미리미리 문제를 풀지 못한 죄이기 때문에 어쩔 수 없이 패스..ㅠ 근데 문제 풀이를 들으면서 DP 문제에 대해서 조금은 감을 잡은 것 같다. 어떤 문제에 DP 풀이를 써야하는지 조금 감을 잡은 느낌..? 더 많이 연습하면서 익혀야겠지만 이렇게 조금씩 성장한다고 느끼는 것은 정말 좋은 것 같다 (\*´︶｀\*)  
<br/>
<br/>

## 1. 문제

도둑이 어느 마을을 털 계획을 하고 있습니다. 이 마을의 모든 집들은 아래 그림과 같이 동그랗게 배치되어 있습니다.

![houses](https://grepp-programmers.s3.amazonaws.com/files/ybm/e7dd4f51c3/a228c73d-1cbe-4d59-bb5d-833fd18d3382.png){:width="300" class="normal"}

각 집들은 서로 인접한 집들과 방범장치가 연결되어 있기 때문에 인접한 두 집을 털면 경보가 울립니다.

각 집에 있는 돈이 담긴 배열 money가 주어질 때, 도둑이 훔칠 수 있는 돈의 최댓값을 return 하도록 solution 함수를 작성하세요.

### 제한조건

- 이 마을에 있는 집은 3개 이상 1,000,000개 이하입니다.
- money 배열의 각 원소는 0 이상 1,000 이하인 정수입니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. 첫번째 집을 털 때와 털지 않을 때를 나누어 사이즈가 money 크기인 두 벡터를 0으로 초기화하여 만든다.
2. include_first 벡터는 첫번째 집부터 해당 인덱스의 집까지 범위로 두고 털수 있는 최댓값이고, exclude_first 벡터는 두번째 집부터 해당 인덱스 집까지 범위로 두고 털수 있는 최댓값이다.
3. include_first 벡터는 첫번째 집을 터는 경우이기 때문에 인덱스 1에 첫번째 집의 돈을 넣는다.  
   (인덱스 1에 넣는 이유는 이후 i번째 집을 포함했을 경우 i-2번째 집까지 최댓값과 더하여 i-1번째 집까지 최댓값과 비교해야하는데 i가 1일 경우 i-2는 범위를 벗어나므로 0번째 인덱스는 0 값으로 채워주고 인덱스 1부터 넣어줘야 한다)
4. 첫번째 집을 터는 경우, 맨 마지막 집은 털 수 없으므로 실제로 확인할 부분은 1~(i-1)까지의 범위가 된다.
5. 첫번째 집을 털지 않는 경우, 두번째 집부터 마지막집까지 털 수 있으므로 확인할 부분은 2~i까지의 범위가 된다.
6. 각 범위를 위와 같이 잡고, money의 각 원소를 반복하면서 include_first와 exclude_first 벡터를 채운다.
7. 첫번째 집부터 해당 인덱스의 집까지에서 털 수 있는 최댓값은 해당 인덱스의 집을 털었을 경우와 털지 않았을 경우를 나누어 큰 값을 고르는 것이다.  
   해당(i) 집을 털었을 경우, 이전(i-1) 집은 털 수 없으므로 전전(i-2) 최댓값과 현재(i) 돈을 합한 값이 최대가되고,  
   해당(i) 집을 털지 않았을 경우, 이전(i-1) 최댓값이 최대가 되므로 두 값을 비교하여 더 큰 값을 해당(i) 에 넣는다.
8. 반복문이 끝나고, include_first 벡터와 exclude_first 벡터의 마지막 값을 비교하여 더 큰 값을 반환한다.  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <vector>

using namespace std;

int solution(vector<int> money) {
    vector<int> include_first(money.size(), 0);
    vector<int> exclude_first(money.size(), 0);

    include_first[1] = money[0];
    for (int i = 1; i < money.size()-1; i++) {
        if (include_first[i] > money[i] + include_first[i-1]) include_first[i+1] = include_first[i];
        else include_first[i+1] = money[i] + include_first[i-1];
    }

    for (int i = 1; i < money.size(); i++) {
        if(i == 1) exclude_first[i] = money[i];
        else if (exclude_first[i-1] > money[i] + exclude_first[i-2]) exclude_first[i] = exclude_first[i-1];
        else exclude_first[i] = money[i] + exclude_first[i-2];
    }

    return max(include_first[money.size()-1], exclude_first[money.size()-1]);
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- 어떤 문제에 DP를 적용해야하는지
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- [Algo Rhythm🕺💃] 프로그래머스 고득점 kit 도둑질 <https://alinew.tistory.com/70>
  > - 해당 문제의 알고리즘 풀이 설명해준 친구 블로그!

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
