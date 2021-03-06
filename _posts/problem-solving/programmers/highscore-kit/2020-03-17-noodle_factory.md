---
title: "프로그래머스 고득점 Kit : 라면공장"
date: 2020-03-17
author: YuJin Kim
categories: [Problem Solving, Programmers, Highscore Kit]
tags: [programmers, highscore kit, level2, algorithm, heap, c++]
sitemap:
  changefreq: daily
---

본 문제는 풀면서 난이도가 조금 있는 것 같은 문제라고 생각했는데, 생각보다 빨리 그리고 생각보다 잘 푼 것 같아서 기분이 좋았다. 근데 처음 풀고 문제를 제출 했을 때 테스트 케이스 몇 개가 틀렸었는데, 경계값들을 조금씩 바꾸면서 제출하니 통과되었다. 풀 때는 맞추기만하면 되니까 넘겼었는데 지금 블로그를 정리하려고 보니 제한조건이 조금 잘못 나와있는 듯해서 그 부분도 같이 언급하려한다.  
<br/>
<br/>

## 1. 문제

라면 공장에서는 하루에 밀가루를 1톤씩 사용합니다.  
원래 밀가루를 공급받던 공장의 고장으로 앞으로 k일 이후에야 밀가루를 공급받을 수 있기 때문에 해외 공장에서 밀가루를 수입해야 합니다.

해외 공장에서는 향후 밀가루를 공급할 수 있는 날짜와 수량을 알려주었고,  
라면 공장에서는 운송비를 줄이기 위해 최소한의 횟수로 밀가루를 공급받고 싶습니다.

현재 공장에 남아있는 밀가루 수량 stock, 밀가루 공급 일정(dates)과 해당 시점에 공급 가능한 밀가루 수량(supplies), 원래 공장으로부터 공급받을 수 있는 시점 k가 주어질 때, 밀가루가 떨어지지 않고 공장을 운영하기 위해서 최소한 몇 번 해외 공장으로부터 밀가루를 공급받아야 하는지를 return 하도록 solution 함수를 완성하세요.

dates[i]에는 i번째 공급 가능일이 들어있으며, supplies[i]에는 dates[i] 날짜에 공급 가능한 밀가루 수량이 들어 있습니다.

### 제한조건

- <span style="color: #c9c9c9">stock에 있는 밀가루는 오늘(0일 이후)부터 사용됩니다.</span>
- stock과 k는 2 이상 100,000 이하입니다.
- dates의 각 원소는 1 이상 k 이하입니다.
- supplies의 각 원소는 1 이상 1,000 이하입니다.
- dates와 supplies의 길이는 1 이상 20,000 이하입니다.
- <span style="color: #c9c9c9">k일 째에는 밀가루가 충분히 공급되기 때문에 k-1일에 사용할 수량까지만 확보하면 됩니다.</span>
- dates에 들어있는 날짜는 오름차순 정렬되어 있습니다.
- <span style="color: #c9c9c9">dates에 들어있는 날짜에 공급되는 밀가루는 작업 시작 전 새벽에 공급되는 것을 기준으로 합니다.  
  예를 들어 9일째에 밀가루가 바닥나더라도, 10일째에 공급받으면 10일째에는 공장을 운영할 수 있습니다.</span>
- 밀가루가 바닥나는 경우는 주어지지 않습니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. `priority_queue`를 생성한다.
2. `stock`에 계속해서 공급받은 밀가루를 더해줄 것이기 때문에 (`k` - `stock`)이 0보다 큰 동안 반복한다.  
   (`k` - `stock`이 0보다 작거나 같아지는 순간에 더 이상 밀가루를 공급 받지 않고 k일까지 버틸 수 있는 시점이 된다)
3. `stock` 갯수 만큼 버틸 수 있기 때문에 `stock` 갯수 보다 작거나 같은 날짜의 `supplies`를 전부 `priority_queue`에 넣는다.
4. `priority_queue` 안의 숫자들이 `stock`으로 버틸 수 있는 동안 새로 공급 받을 수 있는 밀가루 수량들이다.
5. 그 중 가장 많이 공급 받을 수 있는 밀가루인 `priority_queue`의 `top()`을 pop한다.
6. pop한 밀가루만큼을 공급받았다고 생각하고 `answer`를 증가시키고 그 값만큼 `stock`에 더해준다.
7. 반복문이 끝날 때까지 위 과정을 반복하고, 끝나면 `answer`를 반환한다.  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <vector>
#include <queue>

using namespace std;

int solution(int stock, vector<int> dates, vector<int> supplies, int k) {
    priority_queue<int> pq;
    int answer = 0;
    int i = 0;

    while(k - stock > 0) {
        while(stock + 1 > dates[i]) {
            pq.push(supplies[i]);
            i++;
        }

        stock += pq.top();
        pq.pop();
        answer ++;
    }

    return answer;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- 제한조건이 이상하다고 생각한 문항은 회색으로 표시
- 오늘(0일 이후)부터이고 1일부터 시작하고 k일 째는 고려하지 않아도 된다고 했기 때문에 나는 k-1까지라고 생각
- 근데 0일부터 k-1일 까지라고 생각하면 위의 두 회색 문항은 맞는 말이 될듯..
- `priority_queue` 쓰는 법
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- [C++ 공식문서] std:priority_queue:priority_queue <http://www.cplusplus.com/reference/queue/priority_queue/priority_queue/>
  > - 그냥 벡터를 생성할 때와 마찬가지로 생성
- [C++ 공식문서] std:priority_queue:push <http://www.cplusplus.com/reference/queue/priority_queue/push/>
  > - 그냥 `push()` 를 사용해서 push

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
