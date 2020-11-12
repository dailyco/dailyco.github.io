---
title: "프로그래머스 고득점 Kit : 디스크 컨트롤러"
date: 2020-07-15
author: YuJin Kim
categories: [Programmers, Highscore Kit]
tags: [programmers, highscore kit, level3, algorithm, heap, c++]
# sitemap:
#     changefreq: daily
---

이 문제 진짜 오랫동안 풀었다... 풀 수 있을 것 같은데 계속 안풀려서 스트레스도 엄청 받고ㅠㅠ 끝내 2시간만에 풀어냈지만.. 문제에서 효율성 테스트는 없었지만, 정확도 테스트 케이스 자체에서 효율성까지 함께 채점되는 듯한 느낌이었다. 처음에 세웠던 알고리즘은 시간초과해서 풀리지 않은 테스트 케이스들이 꽤 많았기 때문에.. 여튼, 끝내 풀어냈지만 더 공부가 많이 필요한 유형인 것 같다.  
<br/>
<br/>

## 1. 문제

하드디스크는 한 번에 하나의 작업만 수행할 수 있습니다.  
디스크 컨트롤러를 구현하는 방법은 여러 가지가 있습니다.  
가장 일반적인 방법은 요청이 들어온 순서대로 처리하는 것입니다.

예를들어,

```
- 0ms 시점에 3ms가 소요되는 A작업 요청
- 1ms 시점에 9ms가 소요되는 B작업 요청
- 2ms 시점에 6ms가 소요되는 C작업 요청
```

와 같은 요청이 들어왔습니다. 이를 그림으로 표현하면 아래와 같습니다.  
![disk_controller1](https://grepp-programmers.s3.amazonaws.com/files/production/b68eb5cec6/38dc6a53-2d21-4c72-90ac-f059729c51d5.png){:width="500" class="normal"}

한 번에 하나의 요청만을 수행할 수 있기 때문에 각각의 작업을 요청받은 순서대로 처리하면 다음과 같이 처리 됩니다.

![disk_controller2](https://grepp-programmers.s3.amazonaws.com/files/production/5e677b4646/90b91fde-cac4-42c1-98b8-8f8431c52dcf.png){:width="500" class="normal"}

```
- A: 3ms 시점에 작업 완료 (요청에서 종료까지 : 3ms)
- B: 1ms부터 대기하다가, 3ms 시점에 작업을 시작해서 12ms 시점에 작업 완료(요청에서 종료까지 : 11ms)
- C: 2ms부터 대기하다가, 12ms 시점에 작업을 시작해서 18ms 시점에 작업 완료(요청에서 종료까지 : 16ms)
```

이 때 각 작업의 요청부터 종료까지 걸린 시간의 평균은 10ms(= (3 + 11 + 16) / 3)가 됩니다.  
<br/>

하지만 A → C → B 순서대로 처리하면  
![disk_controller3](https://grepp-programmers.s3.amazonaws.com/files/production/9eb7c5a6f1/a6cff04d-86bb-4b5b-98bf-6359158940ac.png){:width="500" class="normal"}

```
- A: 3ms 시점에 작업 완료(요청에서 종료까지 : 3ms)
- C: 2ms부터 대기하다가, 3ms 시점에 작업을 시작해서 9ms 시점에 작업 완료(요청에서 종료까지 : 7ms)
- B: 1ms부터 대기하다가, 9ms 시점에 작업을 시작해서 18ms 시점에 작업 완료(요청에서 종료까지 : 17ms)
```

이렇게 A → C → B의 순서로 처리하면 각 작업의 요청부터 종료까지 걸린 시간의 평균은 9ms(= (3 + 7 + 17) / 3)가 됩니다.  
<br/>

각 작업에 대해 [작업이 요청되는 시점, 작업의 소요시간]을 담은 2차원 배열 jobs가 매개변수로 주어질 때,  
작업의 요청부터 종료까지 걸린 시간의 평균을 가장 줄이는 방법으로 처리하면 평균이 얼마가 되는지 return 하도록 solution 함수를 작성해주세요. (단, 소수점 이하의 수는 버립니다)

### 제한조건

- jobs의 길이는 1 이상 500 이하입니다.
- jobs의 각 행은 하나의 작업에 대한 [작업이 요청되는 시점, 작업의 소요시간] 입니다.
- 각 작업에 대해 작업이 요청되는 시간은 0 이상 1,000 이하입니다.
- 각 작업에 대해 작업의 소요시간은 1 이상 1,000 이하입니다.
- 하드디스크가 작업을 수행하고 있지 않을 때에는 먼저 요청이 들어온 작업부터 처리합니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. 현재 요청 들어온 작업을 담는 우선순위 큐 pq, 작업 시간들의 합 answer, 작업들의 인덱스 i.
2. 작업을 요청 시간이 빠른 순으로, 요청 시간이 같을 경우 소요시간이 짧은 순으로 정렬한다.
3. 더 이상 들어올 요청이 없고, 지금까지 요청 들어온 작업도 없을 때까지 다음을 반복한다.  
   (더 이상 들어올 요청이 없고, 지금까지 요청 들어온 작업도 없다: i == jobs.size() && !pq.size())
4. 현재 요청이 들어온 작업이 없고, 요청 받을 작업이 남아있으면, 현재 시간을 해당 작업 요청 시간으로 설정하고 해당 작업을 큐에 넣어준다.  
   (현재 요청이 들어온 작업이 없다: pq, 요청 받을 작업이 남아있다: i < jobs.size(),  
   하드디스크가 작업을 수행하고 있지 않을 때 다음에 들어올 요청을 바로 수행하기 위해서)
5. 큐에 요청이 들어온 작업이 존재하면, 제일 시간이 적게 걸리는 작업을 하나 꺼내어 현재 시간에 해당 작업 시간을 더해 작업을 끝내준다.
6. answer에 해당 작업을 수행하는데 걸린 시간을 더해주고, 해당 작업을 수행하는 동안 들어온 요청을 큐에 넣어준다.
7. 반복이 끝나고, 평균 작업 시간을 구하기 위해 작업 시간들의 합 answer를 작업 수 i로 나눈 값을 반환한다.  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <algorithm>
#include <vector>
#include <queue>

using namespace std;

int solution(vector<vector<int>> jobs) {
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
    int answer = 0;
    int ms = 0;
    int i = 0;

    sort(jobs.begin(), jobs.end());
    while(true) {
        if (!pq.size() && i < jobs.size()) {
            ms = jobs[i][0];
            pq.push(make_pair(jobs[i][1], jobs[i][0]));
            i++;
        }

        if(pq.size()) {
            pair<int, int> p = pq.top();
            pq.pop();
            ms += p.first;
            answer += ms - p.second;
            while(i < jobs.size() && ms >= jobs[i][0]) {
                pq.push(make_pair(jobs[i][1], jobs[i][0]));
                i++;
            }
        }

        if (i == jobs.size() && !pq.size()) break;
    }

    return answer/i;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- 우선순위 큐의 원소로 pair도 사용 가능
- 우선순위 큐를 min-queue, max-queue로 설정하는 방법
- 오래 걸려서 풀었지만 그래도 결과가 나쁘지 않을 것 같아 기분이 좋다
- 이 문제의 중요 포인트는 현재 시간이 1ms 씩 증가되도록 하는 것이 아닌 처리해야할 요청이 없을 때 바로바로 다음 요청을 가지고 처리하도록 하는 것과 들어온 요청 작업을 바로 끝내고 작업을 처리하는 동안 들어온 다른 요청 작업들을 우선순위 큐에 넣어주는 것
- 즉, 반복문 내에서 쓸데없이 계속해서 반복문이 돌지 않도록 해주는 것!
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- sort 사용법 + priority_queue에서의 sort 방식 차이  
  <https://coding-insider.tistory.com/entry/sort-사용법-priorityqueue에서의-sort-차이>
  > - 우선순위 큐에서 pair를 사용하기 위해서는 선언시에 첫번째 인자로 원소의 자료형, 두번째 인자로 구현체, 세번째 인자로 비교 연산자를 넣어 사용
  > - 비교 연산자에 따라서 max-heap, min-heap이 결정되어진다.

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
