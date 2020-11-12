---
title: "프로그래머스 고득점 Kit : 완주하지 못한 선수"
date: 2020-03-03
author: YuJin Kim
categories: [Programmers, Highscore Kit]
tags: [programmers, highscore kit, level1, algorithm, hash, c++, javascript]
# sitemap:
#     changefreq: daily
---

본 문제는 한 번 풀어본 적이 있어서 문제를 푸는 데에 많은 시간이 걸리지는 않았다. 하지만 C++을 사용해서 문제를 해결하는 것이 처음이었고, 처음에 hash_map으로 잘못 검색하여 실행시키는데 오류 범벅인 코드 덕에 애를 조금 먹었다. 그리고 hash에 대한 개념이 완벽하지는 않지만 조금 잡혀가고 있는 것 같다.  
<br/>
<br/>

## 1. 문제

수많은 마라톤 선수들이 마라톤에 참여하였습니다.  
단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.  
마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.

### 제한조건

- 마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
- completion의 길이는 participant의 길이보다 1 작습니다.
- 참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
- 참가자 중에는 동명이인이 있을 수 있습니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. completion 벡터의 원소를 반복하며 각 원소(완주한 선수 이름)를 name multiset에 넣는다.  
   (multiset은 중복되는 key를 허용)
2. participant 벡터의 원소를 반복하며 각 원소(참여한 선수 이름) 이름을 name multiset에서 찾는다.
3. name multiset에 이름이 없으면 해당 이름을 반환하고, 있으면 multiset에서 해당 이름을 지운다.  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <string>
#include <vector>
#include <set>

using namespace std;

string solution(vector<string> participant, vector<string> completion) {
    multiset<string> names;

    for (int i = 0; i < completion.size(); i++)
        names.insert(completion[i]);

    for (int i = 0; i < participant.size(); i++) {
        multiset<string>::iterator item = names.find(participant[i]);

        if (item == names.end())
            return participant[i];
        else
            names.erase(item);
    }
}
```

<br/>

### [Javascript]

```javascript
function solution(participant, completion) {
  var map = new Array();
  var answer = "";

  participant.forEach(function (p) {
    if (map[p] >= 1) map[p]++;
    else map[p] = 1;
  });

  completion.forEach(function (c) {
    map[c]--;
  });

  for (let key in map) if (map[key] == 1) return key;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- 어떤 문제에 어떤 자료구조를 사용해야하는지 선택의 중요성
- map, set, unordered_map, unordered_set의 차이점
- 다른 사람들의 해결 방법으로 sort 사용 → 여러 방법으로 생각해보는 능력 기르기
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- [C++ 공식문서] std:multiset:find <http://www.cplusplus.com/reference/set/multiset/find/>
- [C++] multiset container 정리 및 사용법 <https://blockdmask.tistory.com/80>
- [연관 컨테이너 - Set, Map, multiSet, multiMap] <https://mrhook.co.kr/84>
- [씹어먹는 C++ - <10 - 2. C++ STL - 셋(set), 맵(map), unordered_set, unordered_map>] <https://modoocode.com/224>

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
