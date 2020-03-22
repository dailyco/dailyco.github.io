---
layout: post
title: "프로그래머스 코딩테스트 고득점 Kit : [정렬] H-Index"
date: 2020-03-06
categories: 프로그래머스고득점Kit
tags: programmershighscorekit sorting level2 algorithm cplusplus
sitemap:
    changefreq: daily
---

난이도 ★ ★ ☆ ☆ ☆  
본 문제는 문제를 이해하는 데에 무척 오려 걸렸다. 문제를 이해한 후에도 나름의 알고리즘을 세우고 코드를 짰지만 도무지 어느 곳이 잘못된지를 몰라 애를 많이 먹어서 알고리즘을 한 번 뒤엎었던 문제이기도 하다. 처음에 생각했던 알고리즘과 다른 알고리즘으로 문제를 해결한 후에 다른 사람의 코드를 보며 처음 세웠던 알고리즘을 정리해 다시 짜면서 해결코드가 두 가지가 되었는데, 코드를 보면서 알고리즘이 어떻게 다른지 생각해보는 것도 좋은 공부가 될 것 같다 :)  
<br/>

<br/>

## 1. 문제
H-Index는 과학자의 생산성과 영향력을 나타내는 지표입니다.  
어느 과학자의 H-Index를 나타내는 값인 h를 구하려고 합니다.  
[위키백과](https://en.wikipedia.org/wiki/H-index)에 따르면, H-Index는 다음과 같이 구합니다.
어떤 과학자가 발표한 논문 n편 중, h번 이상 인용된 논문이 h편 이상이고 나머지 논문이 h번 이하 인용되었다면 h가 이 과학자의 H-Index입니다.
어떤 과학자가 발표한 논문의 인용 횟수를 담은 배열 citations가 매개변수로 주어질 때, 이 과학자의 H-Index를 return 하도록 solution 함수를 작성해주세요.

### 제한조건
- 과학자가 발표한 논문의 수는 1편 이상 1,000편 이하입니다.
- 논문별 인용 횟수는 0회 이상 10,000회 이하입니다.
<br/><br/><br/>

## 2. 알고리즘! 생각해보자
1) citations을 오름차순으로 정렬한다.  
2) citations을 하나씩 돌면서 인용 횟수와 인용된 논문의 갯수 중 작은 값과 지금까지의 가장 큰 H-Index 중 큰 값을 H-Index의 값으로 설정한다.  
3) citations을 모두 돌고 H-Index 값을 반환한다.  
<br/><br/>

## 3. 해결코드
### [C++]
#### 초반 알고리즘으로 생각했던 코드 (통과X)
```c++
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int solution(vector<int> citations) {
    sort(citations.begin(), citations.end());

    for (int i = 0; i < citations.size(); i++) {
       if (i + 1 >= citations[i])
           return min(i+1, citations[i]);

    return citations.size();
}
```
<br/>

#### 뒤엎은 알고리즘으로 해결한 코드 (통과 O)
```c++
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int solution(vector<int> citations) {
    sort(citations.begin(), citations.end(), greater<int>());

    for (int i = 0; i < citations.size(); i++) {
       h_index = max(h_index, min(citations.size() - i, citations[i]));
    }

    return h_index;
}
```
<br/>

#### 해결 후 다른 사람 코드를 참고해 수정한 코드 (통과 O)
```c++
#include <string>
#include <vector>
#include <algorithm>

using namespace std;

int solution(vector<int> citations) {
    sort(citations.begin(), citations.end(), greater<int>());

    for (int i = 0; i < citations.size(); i++)
       if (i + 1 > citations[i])
           return i;
    
    return citations.size();
}
```
<br/><br/><br/>

## 4. 해결능력UP, 깊이 생각해보기
- 초반에 생각했던 알고리즘이 전체적으로는 맞았지만 놓치고 있는 부분이 조금 있었다  
혹시 나와 같이 생각했다면 테스트 케이스 '[20, 19, 18, 1]'의 경우를 고려해보길 바란다
- 다른 사람 코드를 참고해 수정한 코드에서는 H-Index가 해당 논문의 인용횟수/인용된 논문의 수와 다를 경우를 보장
- vector를 내림차 순으로 sorting하는 법
- max값, min값 구하는 법
<br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و
- [C++] sort algorithm 정리 및 예시 <https://blockdmask.tistory.com/178>
내림차 순으로 sorting하기 위해서는 sort() 함수의 3번째 인자에 greater<int>()함수를 assign
- [C++] 최초값, 최대값 함수 min, max 에 대해서 (클래스, vector 사용법까지) <https://blockdmask.tistory.com/366>
최대값, 최소값을 구하기 위해서는 max(), min() 함수를 사용
<br/><br/><br/>