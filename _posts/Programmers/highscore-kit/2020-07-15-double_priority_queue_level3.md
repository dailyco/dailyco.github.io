---
title: "프로그래머스 고득점 Kit : 이중 우선순위 큐"
date: 2020-07-15
author: YuJin Kim
categories: [Programmers, Highscore Kit]
tags: [programmers, highscore kit, level3, algorithm, heap, c++]
# sitemap:
#     changefreq: daily
---

이전 문제에 비해 이 문제는 빨리 끝나서 좋았다. 그런데 처음에 우선순위 큐를 사용해서 풀려고 했다가 망해서 멀티셋을 사용했는데, 멀티셋에서 내가 잘 모르는 부분에 대해서 끙끙대다가 겨우 해결했다. 힘들긴 했지만 새롭게 알게된 것도 있었고, 앞으로 어떻게 사용해야겠다는 생각이 세워져서 많이 배울 수 있는 문제였다 ˘ڡ˘४  
<br/>
<br/>

## 1. 문제

이중 우선순위 큐는 다음 연산을 할 수 있는 자료구조를 말합니다.

| 명령어 | 수신 탑 (높이)                 |
| ------ | ------------------------------ |
| I 숫자 | 큐에 주어진 숫자를 삽입합니다. |
| D 1    | 큐에서 최댓값을 삭제합니다.    |
| D -1   | 큐에서 최솟값을 삭제합니다.    |

이중 우선순위 큐가 할 연산 operations가 매개변수로 주어질 때, 모든 연산을 처리한 후 큐가 비어있으면 [0,0] 비어있지 않으면 [최댓값, 최솟값]을 return 하도록 solution 함수를 구현해주세요.

### 제한조건

- operations는 길이가 1 이상 1,000,000 이하인 문자열 배열입니다.
- operations의 원소는 큐가 수행할 연산을 나타냅니다.
  - 원소는 “명령어 데이터” 형식으로 주어집니다.- 최댓값/최솟값을 삭제하는 연산에서 최댓값/최솟값이 둘 이상인 경우, 하나만 삭제합니다.
- 빈 큐에 데이터를 삭제하라는 연산이 주어질 경우, 해당 연산은 무시합니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. 우선순위 큐처럼 사용할 멀티셋 pq를 생성한다.
2. operations 벡터의 원소를 반복한다.
3. 명령어가 I일 경우에 뒤 따라오는 숫자를 멀티셋에 넣는다.
4. 명령어가 D이고, 삭제할 원소가 멀티셋에 존재하면 뒤 따라오는 명령어를 확인한다.
5. 이어지는 명령어가 -이면 최소값인 멀티셋의 맨 앞의 원소를 삭제한다.
6. 이어지는 명령어가 -가 아니면 최댓값인 멀티셋의 맨 뒤 원소를 삭제한다.
7. 반복이 끝나고 멀티셋을 확인해 원소가 존재하지 않으면 {0, 0} 를, 원소가 존재하면 {최댓값, 최솟값} 를 반환한다.  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <sstream>
#include <string>
#include <vector>
#include <set>

using namespace std;

int getNum(string str) {
    int num;
    string str_num = str.substr(2);

    stringstream ssInt(str_num);
    ssInt >> num;

    return num;
}

vector<int> solution(vector<string> operations) {
    multiset<int> pq;

    for(string op : operations) {
        if (op[0] == 'I') pq.insert(getNum(op));
        else if (op[0] == 'D' && pq.size()) {
            if (op[2] == '-') pq.erase(pq.begin());
            else pq.erase(--pq.end());
        }
    }

    if (pq.empty()) return {0, 0};
    return {*--pq.end(), *pq.begin()};
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- stringstream 사용하는 방법이 아직 익숙하지 않다
- 문자열의 부분 문자열 추출하는 방법
- 멀티셋에 삽입, 삭제하는 방법 (이터레이터 제대로 사용하기)
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- [C++ 공식문서] std:multiset:erase <https://www.cplusplus.com/reference/set/multiset/erase/>
  > - 멀티셋의 원소를 삭제할 때는 iterator를 인자로 받아 해당 iterator가 가르키는 원소 삭제, `multiset.erase(iterator)` 형식으로 사용
- [C++ 공식문서] std:multiset:insert <https://www.cplusplus.com/reference/set/multiset/insert/>
  > - 멀티셋에 원소를 삽일할 때는 삽입하고자하는 원소를 바로 인자로 넣어 삽입 가능, `multiset.insert(e)` 형식으로 사용
- C++ string을 int로 변경하는 방법 <https://psychoria.tistory.com/709>
  > - `stringstream` 을 사용해서 문자열을 정수로 변환 가능, stringstream을 생성할 때에 인자로 변환하고자하는 문자열을 함께 초기화하고  
  >   shift연산자(`>>`)를 사용하여 정수에 넣는다
- C++ 레퍼런스 - string 의 substr 함수 <https://modoocode.com/235>
  > - 문자열의 부분 문자열을 추출하기 위해서는 간단하게 하나의 시작 인자만 넣어 해당 위치부터 끝까지 부분 문자열을 추출 가능, `string.substr(idx)` 형식으로 사용

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
