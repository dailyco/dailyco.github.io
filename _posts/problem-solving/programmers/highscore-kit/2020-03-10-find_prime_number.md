---
title: "프로그래머스 고득점 Kit : 소수 찾기"
date: 2020-03-10
author: YuJin Kim
categories: [Problem Solving, Programmers, Highscore Kit]
tags: [programmers, highscore kit, level2, algorithm, bruteforce, c++]
sitemap:
  changefreq: daily
---

본 문제는 고민을 많이 했던 문제였다. 완전탐색이기 때문에 효율성을 중요하게 생각하지 않는 알고리즘을 생각해보려고해도 어려웠었는데, 포기하고 이 다음 문제를 풀다가 키 포인트를 잡을 수 있었다. 효율성이 그렇게 좋지는 않지만, 나름 수학 공부도 되고 풀면서 재밌었던 것 같다.  
<br/>
<br/>

## 1. 문제

한자리 숫자가 적힌 종이 조각이 흩어져있습니다.  
흩어진 종이 조각을 붙여 소수를 몇 개 만들 수 있는지 알아내려 합니다.  
각 종이 조각에 적힌 숫자가 적힌 문자열 numbers가 주어졌을 때, 종이 조각으로 만들 수 있는 소수가 몇 개인지 return 하도록 solution 함수를 완성해주세요.

### 제한조건

- numbers는 길이 1 이상 7 이하인 문자열입니다.
- numbers는 0~9까지 숫자만으로 이루어져 있습니다.
- 013은 0, 1, 3 숫자가 적힌 종이 조각이 흩어져있다는 의미입니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. 소수 2, 3의 경우는 따로 `numbers`에 포함 여부를 확인해 `answer`값을 증가시킨다.
2. 6n - 1, 6n + 1 꼴의 자연수가 소수가 맞는지 `is_prime()` 함수를 통해 확인한다.  
   (소수가 맞는지는 해당 수를 (1 ~ 해당 수의 제곱근) 범위의 수들로 나눠서 딱 떨어지는 숫자가 없는 것으로 확인 가능)
3. 소수가 맞으면, `numbers` 카드들로 해당 소수를 만들수있는지 `make_prime_number()` 함수를 통해 확인한다.  
   (소수를 `numbers`에서 한개씩 찾아 없는 수가 있으면 만들 수 없는 것으로, 전부 있으면 만들 수 있는 것으로 확인)
4. 만들수 있으면 `answer`값을 증가시킨다.
5. 6 ~ 9999999 범위의 숫자들 중 6n - 1, 6n + 1 꼴의 자연수가 모두 반복된 후, `answer`를 반환한다.  
   (`numbers`의 길이가 1이상 7이하라고 했으므로)  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <string>
#include <vector>
#include <cmath>

using namespace std;

bool make_prime(string numbers, int prime_number) {
    while(prime_number) {
        int pos = numbers.find(prime_number%10 + 48);
        if (pos == -1)
            return false;
        else {
            numbers.erase(pos, 1);
            prime_number /= 10;
        }
    }

    return true;
}

bool is_prime(int prime) {
    int prime_sqrt = sqrt(prime);

    for (int i = 3; i <= prime_sqrt; i++)
        if (prime % i == 0) return false;

    return true;
}

int solution(string numbers) {
    int answer = 0;

    if (numbers.find(50) != -1) answer++;
    if (numbers.find(51) != -1) answer++;
    for (int i = 6; i <= 9999999; i +=6) {
        if (is_prime(i+1) && make_prime(numbers, i+1)) answer++;
        if (is_prime(i-1) && make_prime(numbers, i-1)) answer++;
    }

    return answer;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- 문자열의 길이가 최대 7이기 때문에 결국 2부터 9999999까지 전부 돌려보는 수밖에...
- 조금이라도 효율성을 좋기 하기 위해 "2, 3을 제외한 모든 소수는 '6n - 1', '6n + 1' 꼴이다"라는 소수의 특징을 사용했다
- 어떤 숫자가 소수인지 확인하는 가장 빠른 알고리즘(으로 알고있는데 확실할진...)은 2부터 해당 숫자의 루트 값까지 1씩 증가시켜 나누어서 나눠 떨어지는 값이 없는 숫자이다
- `stoi()` 함수가 먹지를 않아서 ASCII-code를 이용했다
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- [C++ 정리] 자료형의 크기 및 범위 <http://myblog.opendocs.co.kr/archives/1230>
  > - 9999999까지의 숫자를 나타내는데 int형을 사용해도 될지 확인하기 위해 검색 → 사용 가능!
- [Convert a string to int in C++] <https://www.techiedelight.com/convert-string-to-int-cpp/>
  > - string을 int형으로 나타내기위해 검색했으나 모두 에러 발생... 다른 사람들은 안그러던데 왜 이러지ㅠ
- [ASCII code 활용 : char to int (문자형, 정수형 변환)]  
  <https://m.blog.naver.com/PostView.nhn?blogId=xxsaintxx&logNo=220785227573&proxyReferer=https%3A%2F%2Fwww.google.com%2F>
  > - char to int를 하기 위해서는 48을 빼면된다, 반대는 48을 더하면 되고 :)
- [소수] <https://opentutorials.org/course/1685/9469>
  > - 소수의 특징, "2, 3을 제외한 모든 소수는 '6n - 1', '6n + 1' 꼴이다"
- [C언어/C++] pow, sqrt 함수에 대해서(루트함수, 제곱, 제곱근) <https://blockdmask.tistory.com/307>
  > - 어떤 숫자의 제곱근을 구하기 위해서는 `sqrt()` 함수 사용

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
