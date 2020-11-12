---
title: "프로그래머스 고득점 Kit : 가장 먼 노드"
date: 2020-07-29
author: YuJin Kim
categories: [Problem Solving, Programmers, Highscore Kit]
tags: [programmers, highscore kit, level3, algorithm, graph, c++]
# sitemap:
#     changefreq: daily
---

첫 그래프 문제를 풀었다. 그래프는 첫 문제부터 level3이어서 이번에 처음 푸는데 DFS/BFS 문제를 먼저 접하고 풀어서 그런지 생각보다 괜찮았다. 그래프 문제이긴 했지만 BFS를 사용해서 풀었고, 나는 DFS/BFS 문제도 모두 DFS로 풀었어서 이번에 처음 BFS로 풀면서 확실히 어떤 문제에 DFS/BFS를 적용해야하는지 알게된 것 같다. 그리고 문제를 풀면서 또 느꼈던건 알고리즘 수업을 들으면서 배웠던 것이 다 기억이 안나서... 다시 공부해야겠다고 생각했다..ㅠㅠ 화이팅! (و ˃̵ᴗ˂̵)و  
<br/>
<br/>

## 1. 문제

n개의 노드가 있는 그래프가 있습니다. 각 노드는 1부터 n까지 번호가 적혀있습니다.  
1번 노드에서 가장 멀리 떨어진 노드의 갯수를 구하려고 합니다.  
가장 멀리 떨어진 노드란 최단경로로 이동했을 때 간선의 개수가 가장 많은 노드들을 의미합니다.

노드의 개수 n, 간선에 대한 정보가 담긴 2차원 배열 vertex가 매개변수로 주어질 때,  
1번 노드로부터 가장 멀리 떨어진 노드가 몇 개인지를 return 하도록 solution 함수를 작성해주세요.

### 제한조건

- 노드의 개수 n은 2 이상 20,000 이하입니다.
- 간선은 양방향이며 총 1개 이상 50,000개 이하의 간선이 있습니다.
- vertex 배열 각 행 [a, b]는 a번 노드와 b번 노드 사이에 간선이 있다는 의미입니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. 노드의 방문 여부를 확인하는 `visited` 함수를 `false`로 초기화하여 (노드 수 + 1) 만큼 생성한다.  
   (노드가 1번부터 시작하기 때문에 인덱스 또한 1부터 사용했다)
2. 각 노드의 연결 상태를 나타내는 그래프를 나타내기 위해서 노드 번호를 key, 해당 노드와 연결된 노드의 번호를 value로 하는 `map`을 생성한다.
3. BFS에서 노드의 방문을 확인을 확인하기 위해 큐를 한 개를 생성하고, 정답을 나타내는 변수 `answer`를 생성한다.
4. 노드의 연결 상태를 나타내는 2차원 벡터 edge를 `graph`에 초기화해서 나타낸다.  
   (양 방향이기 때문에 한 edge에 대해 두 개의 노드에 모두 넣어준다)
5. 1번 노드로부터 가장 멀리 떨어진 노드를 찾는 것이기 때문에 처음 시작을 1번 노드로 해주기 위해 큐에 1을 넣는다.
6. `cur_size`는 레벨 당 원소의 수를 나타내는 것으로 현재 레벨0에서 1번 노드 한개 이므로 1로 초기화 해준다.
7. 큐에 원소가 있는 동안 다음을 반복한다.
8. 큐에서 원소를 한 개 꺼내 해당 노드를 방문했으므로 `visited`를 `true`로 바꾸고,  
   해당 노드와 연결된 노드를 하나씩 보면서 아직 방문하지 않았으면 해당 노드를 큐에 넣는다.
9. `cur_size`를 1 감소시키고 해당 변수가 0이 되면 새로운 레벨의 원소가 시작하는 것이므로  
   큐의 원소의 수만큼 다시 `cur_size`를 설정해주고, `answer` 역시 큐의 사이즈로 할당시켜준다.  
   (큐 사이즈가 0이 될 때에는 더 이상 다음 레벨이 없는 것이므로 해당 작업을 하지 않는다!)
10. 반복문이 끝나면, `answer`를 반환한다.  
    <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <vector>
#include <queue>
#include <map>
#include <set>

using namespace std;

int solution(int n, vector<vector<int>> edge) {
    vector<bool> visited(n+1, false);
    map<int, set<int>> graph;
    queue<int> q;
    int answer;

    for(auto e : edge) {
        graph[e[0]].insert(e[1]);
        graph[e[1]].insert(e[0]);
    }

    q.push(1);
    int cur_size = 1;
    while(q.size()) {
        int i = q.front();
        q.pop();

        visited[i] = true;
        for(int node : graph[i]) {
            if(visited[node] == false) {
                visited[node] = true;
                q.push(node);
            }
        }
        if(--cur_size == 0 && q.size() != 0) {
            answer = q.size();
            cur_size = q.size();
        }
    }

    return answer;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- BFS 공부
- `map`의 value 값으로 꼭 `set`을 쓰지 않아도 됐겠다 (`vector` 써도 무방했을 듯!)
- level 별로 원소의 갯수를 구하기 위해 `cur_size` 변수를 사용한 것은 잘한듯ㅎㅎ
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- [알고리즘] 너비 우선 탐색(BFS)이란 <https://gmlwjd9405.github.io/2018/08/15/algorithm-bfs.html>
  > - BFS의 특징은 재귀가 아니라는 것과, 큐를 이용한다는 것!

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
