---
title: "프로그래머스 고득점 Kit : 베스트 앨범"
date: 2020-07-13
author: YuJin Kim
categories: [Problem Solving, Programmers, Highscore Kit]
tags: [programmers, highscore kit, level3, algorithm, hash, c++]
# sitemap:
#     changefreq: daily
---

드디어 첫 level3 문제이다. 문제 자체는 어렵지 않았는데, 좀 더 효율적으로 짜고싶다는 욕심이 생기니까 문제를 풀고나서 더 고민해보면서 시간을 많이 소모한 것 같다. 그런데도 결국 마음에 드는 코드는 나오지 않아서 좀 더 고민해야 할 듯... 알고리즘 공부가 아직 많이 부족한가보다ㅠㅠ 문제를 풀수록 자신감이 생겼는데 이번 부스트 캠프 코딩 테스트에 떨어지고 ʕ ཀ ⌂ ཀ ʔ 다시 자신감이 많이 낮아졌다. 아직 내가 많이 부족하다는 것을 인정하고 더 열심히 해야겠다는 생각이 든다. (사실 알고리즘 공부한지 얼마 되지도 않았는데 자만심이 컸던 것 같다) 앞으로의 나에게 화이팅!  
<br/>
<br/>

## 1. 문제

스트리밍 사이트에서 장르 별로 가장 많이 재생된 노래를 두 개씩 모아 베스트 앨범을 출시하려 합니다. 노래는 고유 번호로 구분하며, 노래를 수록하는 기준은 다음과 같습니다.

```
1. 속한 노래가 많이 재생된 장르를 먼저 수록합니다.
2. 장르 내에서 많이 재생된 노래를 먼저 수록합니다.
3. 장르 내에서 재생 횟수가 같은 노래 중에서는 고유 번호가 낮은 노래를 먼저 수록합니다.
```

노래의 장르를 나타내는 문자열 배열 genres와 노래별 재생 횟수를 나타내는 정수 배열 plays가 주어질 때,  
베스트 앨범에 들어갈 노래의 고유 번호를 순서대로 return 하도록 solution 함수를 완성하세요.

### 제한조건

- genres[i]는 고유번호가 i인 노래의 장르입니다.
- plays[i]는 고유번호가 i인 노래가 재생된 횟수입니다.
- genres와 plays의 길이는 같으며, 이는 1 이상 10,000 이하입니다.
- 장르 종류는 100개 미만입니다.
- 장르에 속한 곡이 하나라면, 하나의 곡만 선택합니다.
- 모든 장르는 재생된 횟수가 다릅니다.
  <br/><br/><br/>

## 2. 알고리즘! 생각해보자

1. `genres` 벡터를 노래의 장르를 key, 해당 장르의 총 play 횟수를 value하는 맵인 `genres_count`에 나누어 넣고,  
   장르를 key, 각 노래의 고유 번호와 play 횟수 쌍을 원소로 갖는 벡터를 value로 하는 맵인 `genres_musics`에도 나누어 넣는다.
2. `genres_count` 맵을 이용해서 반대로 해당 장르의 총 play 횟수를 key로 하고 노래의 장르를 value로 하는 맵 `count_genres`에 바꿔 넣는다.  
   (이 작업을 해주는 이유는 총 play 횟수별로 장르를 정렬해주기 위해서이고, 문제 상에서 모든 장르는 재생된 횟수가 다르다는 제한조건이 있기 때문에 장르의 총 play 횟수가 key 값이 될 수 있다)
3. `genres_musics`맵에서 value값인 벡터를 play 수가 많은 순으로, 같을 경우 고유번호가 작은 순으로 정렬한다.
4. `count_genres`맵의 value 장르 순서대로 `genres_musics`맵의 정렬된 벡터에서 노래 두 곡씩 `answer` 벡터에 담는다. (노래가 한 곡일 경우 한 곡만 담는다)
5. `answer` 벡터에 모든 장르의 노래를 두(한) 곡씩 담은 후, `answer`를 반환한다.  
   <br/><br/>

## 3. 해결코드

### [C++]

```c++
#include <algorithm>
#include <string>
#include <vector>
#include <map>

using namespace std;

bool compare(pair<int, int> a, pair<int, int> b) {
    if (a.second == b.second) return a.first < b.first;
    return a.second > b.second;
}

vector<int> solution(vector<string> genres, vector<int> plays) {
    map<string, int> genres_count;
    map<int, string> count_genres;
    map<string, vector<pair<int, int>>> genres_musics;
    vector<int> answer;

    for (int i = 0; i < genres.size(); i++) {
        genres_count[genres[i]] += plays[i];
        genres_musics[genres[i]].push_back(make_pair(i, plays[i]));
    }

    for (auto it = genres_count.begin(); it != genres_count.end(); it++)
        count_genres[it->second] = it->first;

    for (auto it = genres_musics.begin(); it != genres_musics.end(); it++)
        sort(it->second.begin(), it->second.end(), compare);

    for (auto it = count_genres.rbegin(); it != count_genres.rend(); it++) {
        answer.push_back(genres_musics[it->second][0].first);
        if (genres_musics[it->second].size() > 1) answer.push_back(genres_musics[it->second][1].first);
    }

    return answer;
}
```

<br/><br/>

## 4. 해결능력UP, 깊이 생각해보기

- 더 간단하게 푸는 방법을 고민해봤는데 더 이상 방법이 없는 것 같다..
- 맵의 특징으로 정렬이 자동으로 된다는 것! 기억해 두자
- 문제를 잘 읽고 예외의 경우도 잘 고려해주기
  <br/><br/><br/>

## 5. 참고해서 문제해결 ٩( ᐛ )و

- 없다! v｡◕‿◕｡v

<br/><br/><br/>

```
출처: 프로그래머스 코딩 테스트 연습, https://programmers.co.kr/learn/challenges
```
