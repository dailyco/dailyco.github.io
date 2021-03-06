---
title: "프로그래머스 고득점 Kit : 다리를 지나는 트럭"
date: 2020-03-17
author: YuJin Kim
categories: [Problem Solving, Programmers, Highscore Kit]
tags: [programmers, highscore kit, level2, algorithm, stack-queue, c++]
sitemap:
  changefreq: daily
---

오랜만에 프로그래머스 고득점 Kit 문제를 풀어 올린다. 그동안 자바 캠프에 대해서 정리하느라고 알고리즘 문제 푸는 것을 잠시 쉬었더니 금세 감을 잃었는지 이 문제를 푸는데에는 꽤 오래 걸렸다. 문제 자체를 이해하는 데에도 시간을 많이 썼던 탓도 있긴하지만, 그래도 문제를 풀어놓고보니 나름 잘 풀었다는 생각이 들어서 뿌듯했던 문제였다 :)  
<br/>
<br/>

## 1. 문제

트럭 여러 대가 강을 가로지르는 일 차선 다리를 정해진 순으로 건너려 합니다.  
모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 알아내야 합니다.  
트럭은 1초에 1만큼 움직이며, 다리 길이는 bridge_length이고 다리는 무게 weight까지 견딥니다.  
※ 트럭이 다리에 완전히 오르지 않은 경우, 이 트럭의 무게는 고려하지 않습니다.

예를 들어, 길이가 2이고 10kg 무게를 견디는 다리가 있습니다.  
무게가 [7, 4, 5, 6]kg인 트럭이 순서대로 최단 시간 안에 다리를 건너려면 다음과 같이 건너야 합니다.

| 경과 시간 | 다리를 지난 트럭 | 다리를 건너는 트럭 | 대기 트럭 |
| --------- | ---------------- | ------------------ | --------- |
| 0         | []               | []                 | [7,4,5,6] |
| 1~2       | []               | [7]                | [4,5,6]   |
| 3         | [7]              | [4]                | [5,6]     |
| 4         | [7]              | [4,5]              | [6]       |
| 5         | [7,4]            | [5]                | [6]       |
| 6~7       | [7,4,5]          | [6]                | []        |
| 8         | [7,4,5,6]        | []                 | []        |

따라서, 모든 트럭이 다리를 지나려면 최소 8초가 걸립니다.

solution 함수의 매개변수로 다리 길이 bridge_length, 다리가 견딜 수 있는 무게 weight, 트럭별 무게 truck_weights가 주어집니다. 이때 모든 트럭이 다리를 건너려면 최소 몇 초가 걸리는지 return 하도록 solution 함수를 완성하세요.

### 제한조건

- bridge_length는 1 이상 10,000 이하입니다.
- weight는 1 이상 10,000 이하입니다.
- truck_weights의 길이는 1 이상 10,000 이하입니다.
- 모든 트럭의 무게는 1 이상 weight 이하입니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. 다리를 건너고 있는 트럭과 그 위치를 함께 표현할 수 있도록 `list`를 생성한다.  
   (`list`는 다리 위의 상황을 나타내는 다리 자체로 생각)
2. 트럭의 위치를 표현하기 위해 `list`를 `bridge_length` 만큼 0으로 초기화한다.
3. 현재 다리 위에 있는 트럭의 총 무게를 알기위해 `total_weight` 변수를 생성한다.
4. `list`가 전부 비워질 때까지 다음을 반복한다.
5. 1초가 지나고(`answer`를 1만큼 증가) `list` 안의 원소를 한칸씩 앞으로(`list`에서 맨 앞의 원소를 pop) 이동 시키고, pop한 원소의 무게를 `total_weight`에서 빼준다.
6. 다리를 건너야할 트럭이 남아있고, 트럭이 다리위로 올라가면 무게가 초과되면,  
   `list`에 새로운 트럭이 가지 못했다는 것을 나타내기 위해 0을 push한다.
7. 다리를 건너야할 트럭이 남아있고, 트럭이 다리위로 올라가도 무게를 초과하지 않으면 해당 트럭을 다리 위로 올려준다.  
   (`list`에 트럭 무게 추가, `total_weight`에 해당 트럭 무게만큼 추가, `truck_weights`에서는 해당 원소 삭제)
8. `list`가 비워져 반복이 끝나면 `answer`를 반환한다.  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <vector>
#include <list>

using namespace std;

int solution(int bridge_length, int weight, vector<int> truck_weights) {
    list<int> lst (bridge_length, 0);
    int total_weight = 0;
    int answer = 0;

    while(lst.size()) {
        total_weight -= lst.front();
        lst.pop_front();
        answer++;

        if (truck_weights.size()) {
            if (truck_weights[0] + total_weight > weight) {
                lst.push_back(0);
            } else {
                lst.push_back(truck_weights[0]);
                total_weight += truck_weights[0];
                truck_weights.erase(truck_weights.begin());
            }
        }
    }

    return answer;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- `queue`가 처음에 0으로 원하는 갯수만큼 초기화가 안돼서 다른 자료구조를 찾아보다가 `list` 발견!
- `list` 라는 자료구조가 있다는 것도 처음 알았다...
- `answer` 만큼 `while loop` 이 돌아야하는게 조금 효율성이 안좋다고 생각할 수 있는데... 그럭저럭 괜찮은듯(?!)
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- [C++ 공식문서] std:list <http://www.cplusplus.com/reference/list/list/>

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
