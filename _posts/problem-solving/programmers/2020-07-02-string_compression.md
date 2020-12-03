---
title: "2020 KAKAO BLIND RECRUITMENT : 문자열 압축"
date: 2020-07-02
author: YuJin Kim
categories: [Problem Solving, Programmers, Kakao]
tags: [programmers, level2, algorithm, bruteforce, c++]
sitemap:
  changefreq: daily
---

오늘은 2020 부스트 캠프 1차 온라인 코딩 테스트를 대비해서 실제 시험 환경인 프로그래머스 사이트를 통해 코딩 테스트 준비를 했다. 작년 후기를 통해 문제의 난이도가 그렇게 높지 않다는 것을 듣고 2020, 2019 KAKAO BLIND RECRUITMENT 문제 중 level2 문제 4개를 뽑아 2시간 30분간 시간을 제한해서 문제를 풀었는데, 생각보다 어렵더라... 알고리즘 공부 더 열심히 해야지 o(╥﹏╥)o  
<br/>
<br/>

## 1. 문제

데이터 처리 전문가가 되고 싶은 어피치는 문자열을 압축하는 방법에 대해 공부를 하고 있습니다.  
최근에 대량의 데이터 처리를 위한 간단한 비손실 압축 방법에 대해 공부를 하고 있는데, 문자열에서 같은 값이 연속해서 나타나는 것을 그 문자의 개수와 반복되는 값으로 표현해 더 짧은 문자열로 줄여서 표현하는 알고리즘을 공부하고 있습니다. 간단한 예로 aabbaccc의 경우 2a2ba3c(문자가 반복되지 않아 한번만 나타난 경우 1은 생략함)와 같이 표현할 수 있는데, 이러한 방식은 반복되는 문자가 적은 경우 압축률이 낮다는 단점이 있습니다.

예를 들면, abcabcdede와 같은 문자열은 전혀 압축되지 않습니다.  
어피치는 이러한 단점을 해결하기 위해 문자열을 1개 이상의 단위로 잘라서 압축하여 더 짧은 문자열로 표현할 수 있는지 방법을 찾아보려고 합니다.

예를 들어, ababcdcdababcdcd의 경우 문자를 1개 단위로 자르면 전혀 압축되지 않지만, 2개 단위로 잘라서 압축한다면 2ab2cd2ab2cd로 표현할 수 있습니다. 다른 방법으로 8개 단위로 잘라서 압축한다면 2ababcdcd로 표현할 수 있으며, 이때가 가장 짧게 압축하여 표현할 수 있는 방법입니다.

다른 예로, abcabcdede와 같은 경우, 문자를 2개 단위로 잘라서 압축하면 abcabc2de가 되지만, 3개 단위로 자른다면 2abcdede가 되어 3개 단위가 가장 짧은 압축 방법이 됩니다. 이때 3개 단위로 자르고 마지막에 남는 문자열은 그대로 붙여주면 됩니다.

압축할 문자열 s가 매개변수로 주어질 때, 위에 설명한 방법으로 1개 이상 단위로 문자열을 잘라 압축하여 표현한 문자열 중 가장 짧은 것의 길이를 return 하도록 solution 함수를 완성해주세요.

### 제한조건

- s의 길이는 1 이상 1,000 이하입니다.
- s는 알파벳 소문자로만 이루어져 있습니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. `answer` 값을 문자열 길이로 초기화한다.
2. 문자열은 압축하는 단위의 범위를 1~(문자열 길이/2)로 정하여 아래 내용을 반복한다.
3. 해당 단위만큼 문자열을 나누어 `string_set` 벡터에 담는다.  
   (마지막에 빈 문자열을 push → 후에 벡터의 마지막 원소의 처리를 위해서)
4. `length` 값을 해당 단위만큼 문자열을 나눈 나머지로 초기화한다.
5. `string_set` 크기만큼 아래 내용을 반복한다.
6. 벡터의 이전 원소와 현재 원소가 같으면 `count` 값을 증가시킨다.
7. 원소가 다르고 `count` 값이 1보다 크면 `length`에 `count` 값을 문자열로 변환시키고 그 길이만큼 더한다.  
   (해당 갯수만큼 숫자 뒤에 해당 단위의 문자열이 나오기 때문에)
8. `count` 값이 그대로 1이면 `length`에 해당 단위의 길이만큼 더한다.
9. `string_set` 벡터 반복문이 끝나고 `length` 값이 `answer`보다 작으면 `answer`에 `length` 값을 할당한다.
10. 문자열을 압축하는 단위의 반복문이 끝나고 `answer`를 반환한다.  
    <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <string>
#include <vector>

using namespace std;

int solution(string s) {
    int answer = s.length();

    for(int i = 1; i < s.length()/2 + 1; i++) {
        vector<string> string_set;

        for(int j = 0; j+i-1 < s.length(); j += i)
            string_set.push_back(s.substr(j, i));
        string_set.push_back("");

        int length = s.length() % i;
        int count = 1;
        for(int j = 1; j < string_set.size(); j++) {
            if (string_set[j - 1] == string_set[j]) count++;
            else if (count > 1) {
                length += i + to_string(count).length();
                count = 1;
            } else length += i;
        }

        if (length < answer) answer = length;
    }

    return answer;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- 문자열에서 일부 가져오는 방법
- 정수를 `string`으로 변환하는 방법
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- C++ 레퍼런스 - string의 substr 함수 <https://modoocode.com/235>
  > - 문자열에서 일부 문자열만 가지고 올 때는 `string.substr()` 사용
  > - 첫 번째 파라미터는 시작 인덱스, 두 번째 파라미터는 갯수, 두 번째 파라미터는 생략 가능하며 생략시 문자열의 끝까지 반환
- [C++]to_string 함수에 대해서 (int to string) <https://blockdmask.tistory.com/334>
  > - 정수를 string으로 변환할 때는 `to_string()`을 사용

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
