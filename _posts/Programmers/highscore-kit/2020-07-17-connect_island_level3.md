---
title: "프로그래머스 고득점 Kit : 섬 연결하기"
date: 2020-07-17
author: YuJin Kim
categories: [Programmers, Highscore Kit]
tags: [programmers, highscore kit, level3, algorithm, greedy, c++]
# sitemap:
#     changefreq: daily
---

이 문제는 알고리즘은 어떻게 세워야할지 알겠는데 자료구조를 어떻게 만들어야 효율적으로 풀 수 있을지 엄청 고민했던 문제이다. 결국 그 방법을 찾지 못해서 알고리즘을 뒤엎어 해결했는데 효율성 측면에서 무척 마음에 들지 않는다..ㅠㅠ 기존의 알고리즘으로 해결할 수 있는 방법에 대해서 더 고민해보고 가능하다면 이에 대해서는 추 후에 추가적으로 작성하고싶다 (ง •̀\_•́)ง  
<br/>
<br/>

## 1. 문제

n개의 섬 사이에 다리를 건설하는 비용(costs)이 주어질 때,  
최소의 비용으로 모든 섬이 서로 통행 가능하도록 만들 때 필요한 최소 비용을 return 하도록 solution을 완성하세요.

다리를 여러 번 건너더라도, 도달할 수만 있으면 통행 가능하다고 봅니다.  
예를 들어 A 섬과 B 섬 사이에 다리가 있고, B 섬과 C 섬 사이에 다리가 있으면 A 섬과 C 섬은 서로 통행 가능합니다.

### 제한조건

- 섬의 개수 n은 1 이상 100 이하입니다.
- costs의 길이는 ((n-1) \* n) / 2이하입니다.
- 임의의 i에 대해, costs[i][0] 와 costs[i] [1]에는 다리가 연결되는 두 섬의 번호가 들어있고,  
  costs[i] [2]에는 이 두 섬을 연결하는 다리를 건설할 때 드는 비용입니다.
- 같은 연결은 두 번 주어지지 않습니다. 또한 순서가 바뀌더라도 같은 연결로 봅니다.  
  즉 0과 1 사이를 연결하는 비용이 주어졌을 때, 1과 0의 비용이 주어지지 않습니다.
- 모든 섬 사이의 다리 건설 비용이 주어지지 않습니다. 이 경우, 두 섬 사이의 건설이 불가능한 것으로 봅니다.
- 연결할 수 없는 섬은 주어지지 않습니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. 연결된 섬을 담고있는 ccosts 셋과 세워야하는 다리 갯수를 나타내는 answer 변수를 생성한다.
2. 다리를 건설하는데에 드는 비용이 적은 순으로 costs 벡터를 정렬한다.
3. costs의 첫 원소의 두 섬을 ccosts 셋에 넣고, 해당 비용만큼 answer에 더한다.  
   (처음 원소는 무조건 연결시키고 이 섬들에 한 개씩 연결시키는 식으로 진행)
4. ccosts에 모든 섬이 들어갈 때까지 다음을 반복한다.
5. costs 벡터의 두번째 원소부터 시작해서 두 섬이 이미 ccosts 셋에 있으면 넘어가고, 둘 중 한 섬이 ccosts 셋에 있으면 새로운 섬을 이을 수 있으므로 ccosts에 해당 섬을 넣어주고 그 비용만큼 answer를 증가시킨다.
6. 해당 원소는 벡터에서 지워주고 반복문을 빠져나가 다시 처음부터 벡터를 탐색하면서 이을 수 있는 섬을 찾아준다.
7. 반복문이 끝나면, answer를 반환한다.  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <algorithm>
#include <string>
#include <vector>
#include <set>

using namespace std;

bool compare(vector<int> v1, vector<int> v2) {
    return v1[2] < v2[2];
}

int solution(int n, vector<vector<int>> costs) {
    set<int> ccosts;
    int answer = 0;

    sort(costs.begin(), costs.end(), compare);
    ccosts.insert(costs[0][0]);
    ccosts.insert(costs[0][1]);
    answer += costs[0][2];

    while(ccosts.size() < n) {
        for(int i = 1; i < costs.size(); i++) {
            if (ccosts.find(costs[i][0]) != ccosts.end()
                && ccosts.find(costs[i][1]) != ccosts.end()) continue;
            if (ccosts.find(costs[i][0]) != ccosts.end()
                || ccosts.find(costs[i][1]) != ccosts.end()) {
                ccosts.insert(costs[i][0]);
                ccosts.insert(costs[i][1]);
                answer += costs[i][2];
                costs.erase(costs.begin() + i);
                break;
            }
        }
    }

    return answer;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- 셋에서 원소 탐색 방법
- 이 방법보다 더 좋을 알고리즘을 생각해서 다시 짜보자!
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- [C++ 공식문서] std:set:find <https://www.cplusplus.com/reference/set/set/find/>
  > - 셋의 원소를 찾을 때에는 `find()` 를 사용, 찾는 원소가 없을 경우에는 해당 셋의 마지막 원소 `set.end()`를 반환

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
