---
title: "프로그래머스 고득점 Kit : 입국심사"
date: 2020-07-31
author: YuJin Kim
categories: [Programmers, Highscore Kit]
tags: [programmers, highscore kit, level3, algorithm, binary search, c++]
# sitemap:
#     changefreq: daily
---

오늘 이 문제를 풀기 전에 약간 당황했다. 프로그래머스의 문제가 몇 개 사라졌는데 바로 어제 풀었던 '[[이분탐색] 예산]({{site.url}}/posts/buget_level3)' 문제가 사라져 있어서 알게되었다 😅 당황해서 다른 문제들도 몇 개 봤는데 다이나믹 프로그래밍 문제 몇 개 외에도 조금씩 사라졌더라... 잠깐의 오류인지, 아니면 프로그래머스 측에서 아예 문제를 없애버린 건지는 모르겠지만 아직 풀어보지 못한 문제가 하나씩 사라지니 마음이 조금 조급해졌다. 문제가 더 없어지기 전에 하루 빨리 프로그래머스 고득점 kit을 마무리하고싶다! 뽜야! (૭ ᐕ)૭  
<br/>
<br/>

## 1. 문제

n명이 입국심사를 위해 줄을 서서 기다리고 있습니다.  
각 입국심사대에 있는 심사관마다 심사하는데 걸리는 시간은 다릅니다.

처음에 모든 심사대는 비어있습니다. 한 심사대에서는 동시에 한 명만 심사를 할 수 있습니다.  
가장 앞에 서 있는 사람은 비어 있는 심사대로 가서 심사를 받을 수 있습니다.  
하지만 더 빨리 끝나는 심사대가 있으면 기다렸다가 그곳으로 가서 심사를 받을 수도 있습니다.

모든 사람이 심사를 받는데 걸리는 시간을 최소로 하고 싶습니다.

입국심사를 기다리는 사람 수 n, 각 심사관이 한 명을 심사하는데 걸리는 시간이 담긴 배열 times가 매개변수로 주어질 때, 모든 사람이 심사를 받는데 걸리는 시간의 최솟값을 return 하도록 solution 함수를 작성해주세요.

### 제한조건

- 입국심사를 기다리는 사람은 1명 이상 1,000,000,000명 이하입니다.
- 각 심사관이 한 명을 심사하는데 걸리는 시간은 1분 이상 1,000,000,000분 이하입니다.
- 심사관은 1명 이상 100,000명 이하입니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. can_check() 함수는 solution에서 매개변수로 받은 times, n 변수와 심사 시간을 인수로 주고  
   해당 심사 시간에 n명의 심사가 가능하면 true, 못하면 false를 반환하는 함수로, 해당 함수를 먼저 정의해준다.
2. 제한조건이 입국심사를 기다리는 사람이 1 이상 100,000 이하이고 각 심사관이 심사하는데 걸리는 시간은 1,000,000,000분 이하이기 때문에  
   시작값 left를 1, 끝 값 right를 1,000,000,000,000,000,000으로 초기화하여 생성한다.
3. 이분탐색을 위해 left와 right의 중간값을 mid 변수에 초기화하여 생성한다.
4. left가 right보다 작은 동안 다음을 반복해 이분탐색을 진행한다.
5. 심사 시간 mid동안 n명의 심사가 가능하면 mid-1동안 n명 심사가 가능한지 확인해 가능하지 않으면 mid를 반환한다.  
   (mid동안 n명의 심사가 가능하고, mid-1동안 n명의 심사가 불가능해야 mid가 최소 심사시간이라는 의미이므로)
6. mid-1동안 n명 심사가 가능하면 심사 시간이 더 작아질 수 있으므로 right를 mid로 재할당하여 이분탐색을 진행한다.
7. mid동안 n명 심사가 불가능하면 심사시간이 더 커야하므로 left를 mid로 재할당하여 이분탐색을 진행한다.
8. 반복문 내에서 값들이 반환되지만, 반복문이 끝나면 마지막에 mid를 반환해주고 끝낸다.  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <vector>

using namespace std;

bool can_check(int n, vector<int> times, long long total_time) {
    long long total = 0;

    for(int time : times)
        total += total_time / time;

    return n <= total;
}

long long solution(int n, vector<int> times) {
    long long left = 1, right = 1000000000000000000;
    long long mid = right / 2;

    while(left < right) {
        if(can_check(n, times, mid)) {
            if(!can_check(n, times, mid-1)) return mid;
            right = mid;
        } else left = mid;
        mid = (right + left) / 2;
    }

    return mid;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- 정수형 데이터 타입 long long 범위
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- 데이터 형식 범위 <http://melonicedlatte.com/algorithm/2018/03/04/022437.html>
  > - 정수형 데이터 타입 long long 범위는 -9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807 이다.

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
