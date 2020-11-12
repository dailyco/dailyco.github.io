---
title: ABOUT
type: categories
# The About page
# v2.0
# https://github.com/cotes2020/jekyll-theme-chirpy
# © 2017-2019 Cotes Chung
# MIT License
---

<!-- > **Note**: Add Markdown syntax content to file `tabs/about.md` and it will show up on this page. -->

<div id="archives" class="pl-xl-2">
{% for post in site.posts %}
  {% capture this_year %}{{ post.date | date: "%Y" }}{% endcapture %}
  {% capture pre_year %}{{ post.previous.date | date: "%Y" }}{% endcapture %}
  {% if forloop.first %}
    {% assign last_day = "" %}
    {% assign last_month = "" %}
  <span class="lead">{{this_year}}</span>
  <ul class="list-unstyled">
  {% endif %}
    <li>
      <div>
        {% capture this_day %}{{ post.date | date: "%d" }}{% endcapture %}
        {% capture this_month %}{{ post.date | date: "%b" }}{% endcapture %}
        <span class="date day">{{ this_day }}</span>
        <span class="date month small text-muted">{{ this_month }}</span>
        <a href="{{ post.url | relative_url }}">{{ post.title }}</a>
      </div>
    </li>
  {% if forloop.last %}
  </ul>
  {% elsif this_year != pre_year %}
  </ul>
  <span class="lead">{{pre_year}}</span>
  <ul class="list-unstyled">
    {% assign last_day = "" %}
    {% assign last_month = "" %}
  {% endif %}
{% endfor %}
</div>

─────────────── ✧ʕ·͡˔·ོʔ✧ ───────────────
{: style="text-align: center;"}
![my_photo](/assets/img/sample/myphoto.jpeg){: width="300"}

👩🏻‍💻 Daily CO = 매일 COMMIT, 매일 CODING 👩🏻‍💻
{: style="text-align: center;"}
─────────────── ✧U¯¯¯U✧ ───────────────
{: style="text-align: center;"}
<br/>

<br/>

---

## 🙍🏻‍♀️ 경험 🙍🏻‍♀️
{: style="text-align: center;"}
<br>

- 2017.03 ~ ing ㅤ[Handong global university 입학](http://www.handong.edu/eng/)
- 2017.11 ~ ing ㅤ컴퓨터 공학 전공 시작
- 2018.03 ~ ing ㅤ[전산 동아리 CRA](https://cra16.github.io/)
- 2018.06 ~ 2018.07 ㅤ[김호준 교수님 Java Camp]({{site.url}}/javacamp/2020/03/14/JavaCamp_%EA%B0%9C%EC%9A%94.html)
- 2018.07 ~ 2020.06 ㅤ[남재창 교수님 ISEL 랩실](https://isel.handong.edu)
- 2018.07 ~ 2018.08 ㅤWrongIncrementerChecker Tool 개발
- 2018.08 ㅤ카카오 코드 페스티벌 예선 경험
- 2018.10 ㅤ2018 ACM-ICPC 한국 대학생 프로그래밍 경시대회 예선 경험
- 2018.12 ~ 2019.02 ㅤ[수강신청 도움 웹 Histime 개발](https://github.com/cra16/histime)
- 2019.01 ㅤKCSE 한국 소프트웨어공학 학술대회
  - "버그 검출 규칙 개선을 위한 코드 문맥 수집 방법에 대한 연구" 단편 논문 수상
- 2019.04 ~ 2019.05 ㅤTrello 프로그램 CLI화 Drello 프로그램 개발
- 2019.05 ㅤ대경권 대학생 프로그램 경진대회 예선 경험
- 2019.10 ㅤ교내 TOPCIT 성적 우수 장학생 장려상 수상
- 2019.10 ㅤ2019 ACM-ICPC 한국 대학생 프로그래밍 경시대회 교내 은상 수상
- 2019.11 ㅤ교내 SW 페스티벌 경진대회 스마트 애플리케이션 부문 최우수상 수상
- 2020.01ㅤ "버그 검출 규칙 개선을 위한 코드 문맥 수집 방법" 특허 출원
- 20219.11 ~ㅤ대경권 공공기관 JobGate 어플리케이션 개발
- 2020.09 ~ 2020.11 ㅤ[HAPPY ENDING 프로젝트 개발]({{site.url}}/happy-ending/)
  <br/>
  <br/>

---

## 💻 프로젝트 💻
{: style="text-align: center;"}
<br/>

* 김호준 교수님 Java Camp
* WrongIncrementerChecker Tool
* 수강신청 도움 웹 Histime
* 프로젝트 관리 Trello 프로그램 CLI화 프로그램 Drello
* 지역 선도 사업 대경권 공공기관 Job Gate
* HAPPY ENDING
<br/>
<br/>

---
