---
title: "프로그래머스 고득점 Kit : 저울"
date: 2020-07-18
author: YuJin Kim
categories: [Programmers, Highscore Kit]
tags: [programmers, highscore kit, level3, algorithm, greedy, c++]
# sitemap:
#     changefreq: daily
---

이 문제는 결과적으로 문제를 푸는 데에는 그렇게 많은 시간이 걸리지 않았다. 그런데 처음 세웠던 알고리즘이 탐욕법을 사용하는 알고리즘도 아니었고, 정확도는 다 맞으나 효율성이 하나도 맞지 않아서 다른 알고리즘을 생각해야했다. 그래서 질문하기 게시판(?)에서 '정렬한 배열을 잘 이용해서 풀어보세요'라는 힌트를 얻었고, 이 말을 기반으로 머리를 굴리다가 효율성이 정말 좋은 알고리즘을 생각해냈다. 생각해내고 나서는 정말 뿌듯했는데, 힌트를 얻어 풀었다는 것이 조금 아쉬운 것 같다 (´.\_.`)  
<br/>
<br/>

## 1. 문제

하나의 양팔 저울을 이용하여 물건의 무게를 측정하려고 합니다.  
이 저울의 양팔의 끝에는 물건이나 추를 올려놓는 접시가 달려 있고, 양팔의 길이는 같습니다.  
또한, 저울의 한쪽에는 저울추들만 놓을 수 있고, 다른 쪽에는 무게를 측정하려는 물건만 올려놓을 수 있습니다.

![balance](https://grepp-programmers.s3.amazonaws.com/files/production/f73e61d4de/f4abf5ff-1956-4e49-bd4a-d3d24619bbf0.png){:width="300" class="normal"}

저울추가 담긴 배열 weight가 매개변수로 주어질 때,  
이 추들로 측정할 수 없는 양의 정수 무게 중 최솟값을 return 하도록 solution 함수를 작성해주세요.

예를 들어, 무게가 각각 [3, 1, 6, 2, 7, 30, 1]인 7개의 저울추를 주어졌을 때,  
이 추들로 측정할 수 없는 양의 정수 무게 중 최솟값은 21입니다.

### 제한조건

- 저울추의 개수는 1개 이상 10,000개 이하입니다.
- 각 추의 무게는 1 이상 1,000,000 이하입니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. 저울추들로 측정할 수 있는 최대 무게값을 갖는 answer 변수를 생성한다.
2. weight 벡터를 저울추 무게가 오름차순이 되도록 정렬한다.
3. 벡터의 원소를 한개씩 돌면서 현재까지 측정 가능한 저울추들의 최대 무게값 answer보다 크면 반복을 멈춘다.
4. 벡터의 원소가 (answer+1)보다 크지 않으면 answer에 해당 원소 값만큼을 더한다.
   - 3, 4 번에서 포인트는 answer 변수가 현재까지 측정 가능한 저울추들의 최대 무게값을 의미한다는 것이다.  
     이 말은 실질적으로 생성가능한 무게들이 (0~answer)라는 것이고, 따라서 weight[i] 원소가 있을때  
     이 값이 (answer+1)보다 같거나 작으면 "weight[i]+1, weight[i]+2, ..., weight[i]+answer"  
     식으로 weight[i]+answer 무게까지 측정 가능하게 된다.)

5. 반복문을 벗어나면, answer+1 값을 반환한다.

<br/><br/>

## 3. 해결코드

### [C++]

#### 정확도 100 효율성 0 코드

```c++
#include <algorithm>
#include <string>
#include <vector>

using namespace std;

int solution(vector<int> weight) {
    int answer = 0;
    int num = 0;

    sort(weight.begin(), weight.end(), greater<int>());
    for(answer = 1; num == 0; answer++) {
        num = answer;
        for(auto w : weight) {
            if(num >= w) num -= w;
            if(num == 0) break;
        }
    }

    return answer-1;
}
```

<br/>

#### 정확도 100 효율성 100 코드

```c++
#include <algorithm>
#include <vector>

using namespace std;

int solution(vector<int> weight) {
    int answer = 0;

    sort(weight.begin(), weight.end());
    for(int i = 0; i < weight.size(); i++) {
        if(answer+1 < weight[i]) break;
        answer += weight[i];
    }

    return answer+1;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- '정렬된 배열'에서 어떻게 숫자들을 만들어낼지 생각해내는 것이 중요 포인트!
- 효율적이고 좋은 알고리즘이 바로바로 생각났으면 좋겠다ㅠㅡㅠ
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- 프로그래머스 문제 질문하기 게시판 외에는 없다!

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
