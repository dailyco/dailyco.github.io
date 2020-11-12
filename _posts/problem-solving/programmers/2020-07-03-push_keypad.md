---
title: "2020 카카오 인턴십 : 키패드 누르기"
date: 2020-07-03
author: YuJin Kim
categories: [Problem Solving, Programmers, Kakao]
tags: [programmers, level1, algorithm, c++]
# sitemap:
#     changefreq: daily
---

해당 문제의 유형은 모르겠다..ㅎㅎ 어떠한 자료구조를 사용한게 아니기도하고 그냥 문제를 보고 특정 유형을 생각하고 알고리즘을 세운게 아니라, '이렇게 이렇게하면 풀릴 것 같은데?'라는 생각으로 해결한 문제이기 때문이다. 처음에 이 문제를 풀 때는 풀이 접근을 잘못했었다. 미리 스마트폰 전화 키패드의 거리를 정의할 생각을 했는데 이것도 엄청 복잡하더라...ㅠㅠ 결국 설거지하면서 계속 생각하다 퍼뜩하고 아이디어가 떠올랐고 그대로 구현하니 풀렸다... =(:з」∠)\_  
<br/>
<br/>

## 1. 문제

스마트폰 전화 키패드의 각 칸에 다음과 같이 숫자들이 적혀 있습니다.

![smartphone_keypad](https://grepp-programmers.s3.ap-northeast-2.amazonaws.com/files/production/4b69a271-5f4a-4bf4-9ebf-6ebed5a02d8d/kakao_phone1.png){: width="300" class="normal"}

이 전화 키패드에서 왼손과 오른손의 엄지손가락만을 이용해서 숫자만을 입력하려고 합니다.  
맨 처음 왼손 엄지손가락은 \* 키패드에 오른손 엄지손가락은 # 키패드 위치에서 시작하며, 엄지손가락을 사용하는 규칙은 다음과 같습니다.

```
1. 엄지손가락은 상하좌우 4가지 방향으로만 이동할 수 있으며 키패드 이동 한 칸은 거리로 1에 해당합니다.
2. 왼쪽 열의 3개의 숫자 1, 4, 7을 입력할 때는 왼손 엄지손가락을 사용합니다.
3. 오른쪽 열의 3개의 숫자 3, 6, 9를 입력할 때는 오른손 엄지손가락을 사용합니다.
4. 가운데 열의 4개의 숫자 2, 5, 8, 0을 입력할 때는 두 엄지손가락의 현재 키패드의 위치에서 더 가까운 엄지손가락을 사용합니다.
   4-1. 만약 두 엄지손가락의 거리가 같다면, 오른손잡이는 오른손 엄지손가락, 왼손잡이는 왼손 엄지손가락을 사용합니다.
```

순서대로 누를 번호가 담긴 배열 numbers, 왼손잡이인지 오른손잡이인 지를 나타내는 문자열 hand가 매개변수로 주어질 때, 각 번호를 누른 엄지손가락이 왼손인 지 오른손인 지를 나타내는 연속된 문자열 형태로 return 하도록 solution 함수를 완성해주세요.

### 제한조건

- numbers 배열의 크기는 1 이상 1,000 이하입니다.
- numbers 배열 원소의 값은 0 이상 9 이하인 정수입니다.
- hand는 "left" 또는 "right" 입니다.
  - "left"는 왼손잡이, "right"는 오른손잡이를 의미합니다.
- 왼손 엄지손가락을 사용한 경우는 L, 오른손 엄지손가락을 사용한 경우는 R을 순서대로 이어붙여 문자열 형태로 return 해주세요.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. '\_', '0', '#' 버튼을 각각 10, 11, 12번으로 생각하고, 처음 왼손/오른손 엄지의 위치는 '\_'/'#' 키패드이기 때문에 처음 왼손과 오른손 엄지 손가락 위치를 10, 12으로 초기화한다.
2. static 변수로 오른손(R)은 1, 왼손(L)은 0을 초기화하고 정답 문자열 `answer`를 빈 문자열로 초기화한다.
3. `numbers` 벡터를 반복하면서 각 원소의 값에 따라 다음을 반복한다.
4. 원소가 숫자 1, 4, 7이면 `answer`에 "L"을 붙이고 현재 왼손 엄지 위치를 해당 번호로 바꿔준다.
5. 원소가 숫자 3, 6, 9면 `answe`r에 "R"을 붙이고 현재 오른손 엄지 위치를 해당 번호로 바꿔준다.
6. 원소가 그 외의 숫자일 때, 숫자가 0이면 11을 더해준다. (처음에 '0'버튼을 11번으로 생각하기로 정했기 때문에)
7. 현재 왼손과 오른손 엄지에서 누르고자하는 버튼까지의 거리를 구한다.  
   (어떻게? → '상/하'로 이동시 숫자가 3차이 나고, '좌/우'로 이동시 숫자가 1차이 나는 것을 이용해서 현재 버튼과 목적지 버튼의 차이값에 각각 3으로 나눈 몫과 나머지 값을 더해주면 거리가된다)
8. 왼손 엄지에서 목적지까지와 오른손 엄지에서 목적지까지 거리가 같으면 어느 손잡이인지 판단해 R, L을 설정한다.
9. 왼손 엄지에서 목적지까지가 더 가까우면 L, 오른손 엄지에서 목적지까지가 더 가까우면 R로 설정한다.
10. R, L을 판단하여 `answer`에 해당 값을 이어붙이고, 사용한 손의 엄지 위치를 목적지 번호로 바꿔준다.
11. `numbers` 벡터의 반복이 끝나면 `answer`를 반환한다.  
    <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <string>
#include <vector>

using namespace std;

string solution(vector<int> numbers, string hand) {
    int cur_L = 10, cur_R = 12;
    static int R = 1, L = 0;
    string answer = "";

    for(int num : numbers) {
        switch(num) {
            case 1: case 4: case 7:
                answer += "L";
                cur_L = num;
                break;
            case 3: case 6: case 9:
                answer += "R";
                cur_R = num;
                break;
            default:
                if (num == 0) num += 11;

                int left_dist = abs(num - cur_L);
                int right_dist = abs(num - cur_R);
                left_dist = (left_dist/3) + (left_dist%3);
                right_dist = (right_dist/3) + (right_dist%3);

                int cur_hand;
                if (left_dist == right_dist) cur_hand = hand == "right"? R : L;
                else if(left_dist < right_dist) cur_hand = L;
                else cur_hand = R;

                if(cur_hand) {
                    cur_R = num;
                    answer += "R";
                } else {
                    cur_L = num;
                    answer += "L";
                }
        }
    }

    return answer;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- 절대값 구하는 함수
- star, hash 버튼을 static 변수로 각각 10, 12로 초기화해서 코드를 작성하면 좀 더 깔끔한 코드가 되지 않을까...
- 현재 왼쪽/오른쪽 엄지 손가락으로부터 목적지 버튼까지 거리 구하는 알고리즘을 잘 세운것 같다 (뿌--듯!)
- 어떤 손가락으로 버튼을 누를지 정해지고, 해당 손가락의 위치와 `answer`를 더할 때 좀 더 효율적인/깔끔한 방법?
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- [C언어/C++] 절대값 함수 abs, fabs에 대해서 <https://blockdmask.tistory.com/335>
  > - 절대값을 구할때는 `abs(num)`를 사용

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
