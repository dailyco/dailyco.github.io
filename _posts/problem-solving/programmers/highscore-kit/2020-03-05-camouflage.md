---
title: "프로그래머스 고득점 Kit : 위장"
date: 2020-03-05
author: YuJin Kim
categories: [Problem Solving, Programmers, Highscore Kit]
tags: [programmers, highscore kit, level2, algorithm, hash, c++, javascript]
# sitemap:
#     changefreq: daily
---

본 문제는 이전에 남자친구와 함께 고민해본 적이 있는 문제여서 무척 빠르게 풀었다. 알고리즘 문제라기 보다는 수학 문제에 가깝고 (이 또한 알고리즘 이긴 하지만...) 문제를 풀면서 고등학교 수학에서 배웠던 경우의 수가 생각나는 문제이다.  
<br/>
<br/>

## 1. 문제

스파이들은 매일 다른 옷을 조합하여 입어 자신을 위장합니다.  
예를 들어 스파이가 가진 옷이 아래와 같고 오늘 스파이가 동그란 안경, 긴 코트, 파란색 티셔츠를 입었다면 다음날은 청바지를 추가로 입거나 동그란 안경 대신 검정 선글라스를 착용하거나 해야 합니다.

| 종류 | 이름                       |
| :--- | :------------------------- |
| 얼굴 | 동그란 안경, 검정 선글라스 |
| 상의 | 파란색 티셔츠              |
| 하의 | 청바지                     |
| 겉옷 | 긴 코트                    |

스파이가 가진 의상들이 담긴 2차원 배열 clothes가 주어질 때 서로 다른 옷의 조합의 수를 return 하도록 solution 함수를 작성해주세요.

### 제한조건

- clothes의 각 행은 [의상의 이름, 의상의 종류]로 이루어져 있습니다.
- 스파이가 가진 의상의 수는 1개 이상 30개 이하입니다.
- 같은 이름을 가진 의상은 존재하지 않습니다.
- clothes의 모든 원소는 문자열로 이루어져 있습니다.
- 모든 문자열의 길이는 1 이상 20 이하인 자연수이고 알파벳 소문자 또는 '\_' 로만 이루어져 있습니다.
- 스파이는 하루에 최소 한 개의 의상은 입습니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. 옷을 종류별로 담기위해 `map`을 한 개 생성한다.
2. `clothes`에서 옷의 종류를 key, 옷의 이름을 value로해서 `map`에 나누어 담는다.
3. 옷의 종류 별로 (옷의 갯수 + 1)한 값을 모두 곱해 전체에서 1을 뺀 값을 반환한다.  
   ((옷의 개수 + 1)은 (각 옷을 선택했을 경우 + 해당 옷의 종류를 아예 입지 않았을 경우 1가지)이고,  
   모두 곱한 전체에서 -1을 한 이유는 아무것도 걸치치 않았을 경우 1가지를 제외한 것이다)  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <string>
#include <vector>
#include <map>

using namespace std;

int solution(vector<vector<string>> clothes) {
    map<string,vector<string>> clothes_map;
    int answer = 1;

    for (int i = 0; i < clothes.size(); i++)
        clothes_map[clothes[i][1]].push_back(clothes[i][0]);

    for (auto it = clothes_map.begin(); it != clothes_map.end(); it++)
        answer *= (it->second).size() + 1;

    return answer - 1;
}
```

<br/>

### [Javascript]

```javascript
function solution(clothes) {
  var map = new Array();
  var answer = 1;

  for (var i = 0; i < clothes.length; i++) {
    if (map[clothes[i][1]] >= 1) map[clothes[i][1]]++;
    else map[clothes[i][1]] = 1;
  }

  for (let m in map) answer *= map[m] + 1;

  return answer - 1;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- 전에 생각해 본적이 있는 문제라서 빨리 해결했다
- 수학을 잘한다면 빨리 풀 수 있는 문제가 아닐까
- value를 `vector`로 해서 해결하는 방법 습득!
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- [C++ STL]map의 value에 여러값을 주기 <http://bitly.kr/Kf1SnSwC>
  > - map의 value값으로 vector가 사용 가능
  > - map에서 key의 value에 접근할 때, `map[key]`와 같이 index에 key값을 넣어주는 것도 가능
- [C++] auto 타입추론에 대해서 <https://blockdmask.tistory.com/384>
  > - `auto` 키워드를 사용해서 for문 등에서 유용하게 사용 가능

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
