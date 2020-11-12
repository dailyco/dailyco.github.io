---
title: "2019 KAKAO BLIND RECRUITMENT : 오픈 채팅방"
date: 2020-07-02
author: YuJin Kim
categories: [Problem Solving, Programmers, Kakao]
tags: [programmers, level2, algorithm, hash, c++]
# sitemap:
# changefreq: daily
---

이 문제는 처음에 문제를 자세히 읽지 않아서 문제를 풀고 디버깅을 했던 문제이다. 문제가 너무 길어서 읽지 않고 넘어간 부분이 좀 있었는데 제한조건은 꼭 제대로 읽어야겠다는 생각을 했다. 문제의 난이도는 그렇게 어렵지 않았지만, 자료구조를 어떻게 구성해서 문제를 풀지를 조금 고민했던 문제같다. 그리고 문제를 풀고나서 다른 사람 풀이를 봤는데 내 알고리즘과 비슷하지만, 코드를 좀 더 깔끔하게 푼 사람이 있어서 많이 배웠고, 변수의 이름을 좀 더 직관적으로 잘 지어야겠다는 생각을 했다 ; )  
<br/>
<br/>

## 1. 문제

카카오톡 오픈채팅방에서는 친구가 아닌 사람들과 대화를 할 수 있는데, 본래 닉네임이 아닌 가상의 닉네임을 사용하여 채팅방에 들어갈 수 있다.

신입사원인 김크루는 카카오톡 오픈 채팅방을 개설한 사람을 위해, 다양한 사람들이 들어오고, 나가는 것을 지켜볼 수 있는 관리자창을 만들기로 했다.

채팅방에 누군가 들어오면 다음 메시지가 출력된다.

```
"[닉네임]님이 들어왔습니다."
```

<br/>
채팅방에서 누군가 나가면 다음 메시지가 출력된다.

```
"[닉네임]님이 나갔습니다."
```

<br/>
채팅방에서 닉네임을 변경하는 방법은 다음과 같이 두 가지이다.  
```
* 채팅방을 나간 후, 새로운 닉네임으로 다시 들어간다.
* 채팅방에서 닉네임을 변경한다.
```
<br/>
닉네임을 변경할 때는 기존에 채팅방에 출력되어 있던 메시지의 닉네임도 전부 변경된다.  
예를 들어, 채팅방에 Muzi와 Prodo라는 닉네임을 사용하는 사람이 순서대로 들어오면 채팅방에는 다음과 같이 메시지가 출력된다.  
```
Muzi님이 들어왔습니다.
Prodo님이 들어왔습니다.
```
<br/>

채팅방에 있던 사람이 나가면 채팅방에는 다음과 같이 메시지가 남는다.

```
Muzi님이 들어왔습니다.
Prodo님이 들어왔습니다.
Muzi님이 나갔습니다.
```

<br/>

Muzi가 나간후 다시 들어올 때, Prodo 라는 닉네임으로 들어올 경우 기존에 채팅방에 남아있던 Muzi도 Prodo로 다음과 같이 변경된다.

```
Prodo님이 들어왔습니다.
Prodo님이 들어왔습니다.
Prodo님이 나갔습니다.
Prodo님이 들어왔습니다.
```

<br/>

채팅방은 중복 닉네임을 허용하기 때문에, 현재 채팅방에는 Prodo라는 닉네임을 사용하는 사람이 두 명이 있다.  
이제, 채팅방에 두 번째로 들어왔던 Prodo가 Ryan으로 닉네임을 변경하면 채팅방 메시지는 다음과 같이 변경된다.

```
Prodo님이 들어왔습니다.
Ryan님이 들어왔습니다.
Prodo님이 나갔습니다.
Prodo님이 들어왔습니다.
```

<br/>

채팅방에 들어오고 나가거나, 닉네임을 변경한 기록이 담긴 문자열 배열 record가 매개변수로 주어질 때, 모든 기록이 처리된 후, 최종적으로 방을 개설한 사람이 보게 되는 메시지를 문자열 배열 형태로 return 하도록 solution 함수를 완성하라.

### 제한조건

- record는 다음과 같은 문자열이 담긴 배열이며, 길이는 1 이상 100,000 이하이다.
- 다음은 record에 담긴 문자열에 대한 설명이다.
  - 모든 유저는 [유저 아이디]로 구분한다.
  - [유저 아이디] 사용자가 [닉네임]으로 채팅방에 입장 - Enter [유저 아이디] [닉네임] (ex. Enter uid1234 Muzi)
  - [유저 아이디] 사용자가 채팅방에서 퇴장 - Leave [유저 아이디] (ex. Leave uid1234)
  - [유저 아이디] 사용자가 닉네임을 [닉네임]으로 변경 - Change [유저 아이디] [닉네임] (ex. Change uid1234 Muzi)
  - 첫 단어는 Enter, Leave, Change 중 하나이다.
  - 각 단어는 공백으로 구분되어 있으며, 알파벳 대문자, 소문자, 숫자로만 이루어져있다.
  - 유저 아이디와 닉네임은 알파벳 대문자, 소문자를 구별한다.
  - 유저 아이디와 닉네임의 길이는 1 이상 10 이하이다.
  - 채팅방에서 나간 유저가 닉네임을 변경하는 등 잘못 된 입력은 주어지지 않는다.
    <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. 유저의 아이디와 닉네임을 담는 `uid_name` 맵을 생성한다.
2. 유저 아이디와 명령에 따른 메세지 쌍을 원소로 갖는 `result_pair` 벡터를 생성한다.
3. 최종 문자열 배열인 `answer` 벡터를 생성한다.
4. `record` 벡터의 크기만큼 아래 내용을 반복한다.
5. 벡터의 원소를 스페이스를 기준으로 split한 결과를 `s1`, `s2`, `s3`에 담는다.
6. `s1`(명령)이 "Enter"일 경우 `uid_name` 에 값을, `result_pair` 에 uid와 명령에 맞는 메세지 쌍을 push 한다.
7. `s1`(명령)이 "Leave"일 경우 `result_pair` 에 uid와 명령에 맞는 메세지 쌍을 push 한다.
8. `s1`(명령)이 "Change"일 경우 `uid_name` 에 값을 넣어준다.
9. `record` 벡터 반복문이 끝나고 `result_pair` 에 있는 원소들을 반복하면서 앞의 uid와 매칭되는 닉네임과 뒤의 메세지를 합쳐 `answer` 에 push 한다.
10. `answer` 를 반환한다.  
    <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <string>
#include <sstream>
#include <vector>
#include <map>

using namespace std;

vector<string> solution(vector<string> record) {
    map<string, string> uid_name;
    vector<pair<string, string>> result_pair;
    vector<string> answer;

    for(auto r : record) {
        istringstream iss(r); // stringstream ss(r);
        string s1, s2, s3;

        getline(iss, s1, ' '); // iss>>s1;
        getline(iss, s2, ' '); // iss>>s2;
        getline(iss, s3, ' '); // iss>>s3;

        if (s1 == "Enter") {
            uid_name[s2] = s3;
            result_pair.push_back(make_pair(s2, "님이 들어왔습니다."));
        } else if (s1 == "Leave") result_pair.push_back(make_pair(s2, "님이 나갔습니다."));
        else if (s1 == "Change") uid_name[s2] = s3;
    }

    for(auto result : result_pair)
        answer.push_back(uid_name[result.first] + result.second);

    return answer;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- `string`을 `split` 하는 방법
- `pair` 사용법
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- [Stack overflow] <https://stackoverflow.com/questions/289347/using-strtok-with-a-stdstring>
> - 문자열을 스페이스 기준으로 split 할 때는 `#include <sstream>`
  > - splite 하고자하는 문자열을 파라미터로 `stringstream` 인스턴스를 생성
  > - `stringstream >> split한 결과 값을 담는 문자열` 명령 사용
- C++ pair 사용하여 쌍으로 값저장 <https://godog.tistory.com/entry/c-vector-and-pair-%EC%82%AC%EC%9A%A9>
  > - pair를 벡터의 원소로 사용할 때는 `vector<pair<type, type>>` 으로 생성 가능하고, pair 쌍을 만들어 저장할 때는 `make_pair()`를 사용

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
