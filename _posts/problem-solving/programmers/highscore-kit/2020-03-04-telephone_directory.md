---
title: "프로그래머스 고득점 Kit : 전화번호 목록"
date: 2020-03-04
author: YuJin Kim
categories: [Problem Solving, Programmers, Highscore Kit]
tags: [programmers, highscore kit, level2, algorithm, hash, c++]
# sitemap:
#     changefreq: daily
---

본 문제는 풀기 전에 알고리즘을 생각하면서 '이렇게하면 될까?'하고 반신반의하며 푼 문제이다. set의 upper_bound에 대해서 제대로 이해하지 못하고 있는 줄 알았는데 막상 이걸 이용해서 문제를 해결하고나니 제대로 이해하고 있었다는 생각이 들었다 :)  
<br/>
<br/>

## 1. 문제

전화번호부에 적힌 전화번호 중, 한 번호가 다른 번호의 접두어인 경우가 있는지 확인하려 합니다.  
전화번호가 다음과 같을 경우, 구조대 전화번호는 영석이의 전화번호의 접두사입니다.

- 구조대 : 119
- 박준영 : 97 674 223
- 지영석 : 11 9552 4421

전화번호부에 적힌 전화번호를 담은 배열 phone_book 이 solution 함수의 매개변수로 주어질 때, 어떤 번호가 다른 번호의 접두어인 경우가 있으면 false를 그렇지 않으면 true를 return 하도록 solution 함수를 작성해주세요.

### 제한조건

- phone_book의 길이는 1 이상 1,000,000 이하입니다.
- 각 전화번호의 길이는 1 이상 20 이하입니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. `phone_book`의 원소를 모두 `set`에 담는다.
2. `set`에서 각 `phone_book` 원소의 `upper bound`를 찾는다.  
   (`upper bound`는 해당 값을 가지는 맨 마지막 원소를 가르킨다)
3. `upper bound`가 마지막 원소일 경우는 pass한다.
4. 각 `phone_book` 원소가 해당 `upper_bound`의 접두어인지 확인한다.  
   (`find()` 함수를 사용해서 해당 문자열을 찾지못하면 -1(npos), 찾으면 위치 인덱스를 반환하는 것을 이용)
5. 접두어(-1(npos)이 아니면)이면 `false`를 반환한다.
6. 접두어가 없어 반복문이 끝나면 `true`를 반환한다.  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <string>
#include <vector>
#include <set>

using namespace std;

bool solution(vector<string> phone_book) {
    set<string> phone_numbers;

    for(int i = 0; i < phone_book.size(); i++)
        phone_numbers.insert(phone_book[i]);

    for(int i = 0; i < phone_book.size(); i++) {
        set<string>::iterator itup = phone_numbers.upper_bound(phone_book[i]);
        if (itup == phone_numbers.end()) continue;
        if ((*itup).find(phone_book[i]) != string::npos)
            return false;
    }

    return true;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- 해시를 사용해서 푼 것이 맞나?
- 정렬을 사용해서 풀 수도 있다!
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- [C++ 공식문서] std:set:upper_bound <http://www.cplusplus.com/reference/set/set/upper_bound/>
- [C++ 레퍼런스 - string 의 find 함수] <https://modoocode.com/241>
  > - `string.find()` 는 찾고자하는 문자(열)이 해당 문자열에 없을경우 `string::npos`를 반환

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
