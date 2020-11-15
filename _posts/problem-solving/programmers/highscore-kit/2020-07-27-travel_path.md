---
title: "프로그래머스 고득점 Kit : 여행 경로"
date: 2020-07-27
author: YuJin Kim
categories: [Problem Solving, Programmers, Highscore Kit]
tags: [programmers, highscore kit, level3, algorithm, dfs-bfs, c++]
# sitemap:
#     changefreq: daily
---

오랜만에 알고리즘 문제 풀이였다. 요즘 자격증 시험 때문에 공부하느라고 알고리즘 문제와 웹 공부를 제대로 하지 못했다. 고새 (일주일도 안되는 짧은 시간) 문제 조금 안풀었다고 머리가 굳은건지 열심히 풀려고 생각했는데 잘 안풀리더라...ㅠㅠ 결국 내 나름의 알고리즘을 세워 코드를 작성하였으나 테스트 케이스의 절반만 맞는 참사(...)를 경험하고, 이리저리 머리를 굴려보았으나 시간적인 한계와 더불어 머리가 더 이상 생각을 거부하는 것 같아 다른 사람의 코드를 참고하기로 결정했다 (｡•́-ก̀｡)  
<br/>
<br/>

## 1. 문제

주어진 항공권을 모두 이용하여 여행경로를 짜려고 합니다. 항상 ICN 공항에서 출발합니다.

항공권 정보가 담긴 2차원 배열 tickets가 매개변수로 주어질 때,  
방문하는 공항 경로를 배열에 담아 return 하도록 solution 함수를 작성해주세요.

### 제한조건

- 모든 공항은 알파벳 대문자 3글자로 이루어집니다.
- 주어진 공항 수는 3개 이상 10,000개 이하입니다.
- tickets의 각 행 [a, b]는 a 공항에서 b 공항으로 가는 항공권이 있다는 의미입니다.
- 주어진 항공권은 모두 사용해야 합니다.
- 만일 가능한 경로가 2개 이상일 경우 알파벳 순서가 앞서는 경로를 return 합니다.
- 모든 도시를 방문할 수 없는 경우는 주어지지 않습니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. 답을 나타내는 벡터 `answer`와 답이 나올 때까지 원소들을 하나씩 더해줄 벡터 `temp`를 생성한다.
2. 2차원 벡터 `tickets`의 방문 여부를 확인할 bool타입 원소 `visit`을 `tickets` 사이즈만큼 초기화해 생성한다.
3. `tickets`을 문자열의 오름차순으로 정렬한다. (2차원 벡터의 오름차순 정렬은 1차적으로 첫번째 원소를 기준으로하며, 첫번째 원소가 같을 경우 두번째 원소, 두번째 원소가 같을 경우 세번째 원소를 기준으로 정렬하는 식으로 적용된다)
4. `dfs` 함수를 사용해 방문하는 공항의 경로를 구한다.
5. `dfs` 함수의 인자로 전해지는 값들을 하나씩 보면, 첫번째 인자는 출발 공항 `from`, 두번째는 처음에 solution에서 인자로 받은 2차원 벡터 `tickets`, 세번째는 tickets의 방문 여부를 확인하는 `visit`, 네번째는 재귀함수를 사용해서 계속해서 답을 만드는 벡터 `temp`, 다음은 정답 벡터 `answer`, 마지막은 현재 tickets에서 방문한 공항들을 나타내는 `cnt` 이다.
6. `dfs` 함수의 자세한 내용을 보면, 먼저 출발 공항을 `temp` 에 넣고 모든 tickets의 공항들을 방문했으면 `temp` 가 정답을 다 구했다는 의미이므로 `answer`에 넘겨주고, true를 반환한다.
7. 아직 공항들을 덜 방문했으면 `tickets` 를 하나씩 돌면서 출발 공항이랑 같은 값을 가지면서 아직 방문하지 않은 공항을 찾고, 해당 공항을 통해서 모든 공항을 방문 가능할 경우 `true`를 반환한다.
8. 아직 `tickets`의 모든 공항을 방문하지 않았는데 더 이상 갈 수 있는 경로가 없을 경우 `temp` 에서 처음에 넣었던 출발 공항을 빼고, `false`를 반환한다.
9. `dfs` 함수를 모두 돌아 방문하는 공항 경로를 다 구하고 나서 `answer` 벡터를 반환한다.  
   <br/><br/>

## 3. 해결코드

### [C++]

#### 정확도 50 코드 (통과 X)

```c++
#include <algorithm>
#include <string>
#include <vector>

using namespace std;

int next_idx(string city, vector<vector<string>> tickets) {
    for(int i = 0; i < tickets.size(); i++)
        if(tickets[i][0] == city) return i;

    return -1;
}

vector<string> dfs(string city, vector<vector<string>> tickets) {
    if(tickets.size() == 1) return {tickets[0][1]};

    int idx = next_idx(city, tickets);
    string next_city = tickets[idx][1];
    tickets.erase(tickets.begin() + idx);
    vector<string> answer = dfs(next_city, tickets);
    answer.push_back(next_city);

    return answer;
}

vector<string> solution(vector<vector<string>> tickets) {
    vector<string> answer;

    sort(tickets.begin(), tickets.end());
    answer = dfs("ICN", tickets);
    answer.push_back("ICN");
    reverse(answer.begin(), answer.end());

    return answer;
}
```

<br/>

#### 다른 사람의 코드 참고 (통과 O)

```c++
#include <algorithm>
#include <string>
#include <vector>

using namespace std;

bool dfs(string from, vector<vector<string>>& tickets, vector<bool>& visit, vector<string>& temp, vector<string>& answer, int cnt) {
    temp.push_back(from);
    if (cnt == tickets.size()) {
        answer = temp;
        return true;
    }

    for (int i=0 ; i<tickets.size() ; i++) {
        if (tickets[i][0] == from && visit[i] == false) {
            visit[i] = true;
            bool success = dfs(tickets[i][1], tickets, visit, temp, answer, cnt+1);
            if (success) return true;
            visit[i] = false;
        }
    }

    temp.pop_back();
    return false;
}

vector<string> solution(vector<vector<string>> tickets) {
    vector<string> answer, temp;
    vector<bool> visit(tickets.size(), false);

    sort(tickets.begin(), tickets.end());
    dfs("ICN", tickets, visit, temp, answer, 0);

    return answer;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- 사실 조금 더 고민했으면 충분히 풀 수 있는 문제였는데 아쉽다
- 다음부터는 시간에 쫓기지 말고 여유롭게 잘 풀길!
- `vector` 두 개를 완전히 합치거나, 부분적으로 합치는 방법
- 벡터의 순서를 역순으로 바꾸는 방법
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- [C++ 공식문서] std:vector:erase <https://www.cplusplus.com/reference/vector/vector/erase/>
  > - 벡터의 원소를 삭제할 때는 `iterator`를 사용해서 삭제 가능, `vector.erase(iterator)` 형식으로 사용
- [C++] insert 함수를 이용하여 vector 합치기 / 벡터(vector) 합치는 법 <https://woo-dev.tistory.com/79>
  > - 벡터 두 개를 합치거나 벡터의 일정 부분을 다른 벡터에 삽입하기 위해 `insert()` 사용,  
  >   `vector1.insert(vector1의 삽입하고자하는 위치, vector2의 삽입 시작 원소 iterator, vector2의 삽입 끝 원소 iterator)` 형식으로 사용
- vector 안의 원소들의 순서를 역순으로 바꾸는 방법 <https://starrykss.tistory.com/597>
  > - 벡터의 순서를 역순으로 바꾸기 위해서는 `reverse() 사용`, '`reverse(vector.begin(), vector.end())`' 형식으로 사용
- [프로그래머스] 여행경로 <https://dailyheumsi.tistory.com/22>
  > - 해당 사이트에서 코드를 참고하였다! •͈ᴗ•͈⋆\*

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
