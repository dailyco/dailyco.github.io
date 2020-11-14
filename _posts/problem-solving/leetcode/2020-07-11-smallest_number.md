---
title: "LeetCode Weekly Contest 196 : Minimum Possible Integer After at Most K Adjacent Swaps On Digits"
date: 2020-07-11
author: YuJin Kim
categories: [Problem Solving, Leetcode, Weekly Contest]
tags: [leetcode, coding test, hard, algorithm, greedy, c++]
# sitemap:
#     changefreq: daily
---

The difficulty of this problem was hard, but when I saw the problem, I thought I could solve. So, I challenged it with curiosity, but the result was a little insufficient. It passed 49 of the total 51 test cases. It's a little lacking, but I hope you focus on the algorithm. And if you know where my code is wrong, please let me know. ´•ﻌ•`  
<br/>
<br/>

## 1. Problem

Given a string num representing the digits of a very large integer and an integer k.  
You are allowed to swap any two adjacent digits of the integer at most k times.  
Return the minimum integer you can obtain also as a string.  
<br/>

**Example1 :**  
![example1](https://assets.leetcode.com/uploads/2020/06/17/q4_1.jpg){: width="550" class="normal"}

> **Input:** num = "4321", k = 4  
> **Output:** "1342"  
> **Explanation:** The steps to obtain the minimum integer from 4321 with 4 adjacent swaps are shown.

<br/>
**Example2 :**

> **Input:** num = "22", k = 22  
> **Output:** "22"

<br/>

### Constraints

- 1 <= num.length <= 30000
- num contains digits only and doesn't have leading zeros.
- 1 <= k <= 10^9
  <br/><br/><br/>

## 2. Thinking Algorithm

1. Create `sorted_num` string which initialize `num` var.
2. Sort the `sorted_num` var in ascending order.
3. Start with the first element of the `sorted_num` var,  
   find its location at `num`, and verify that it can be brought forward.
4. If it can be brought forward, reduce `k` by the number of movements and add it to the `answer` string.
5. For the `num` and `sorted_num` var, erase the corresponding character and repeat the first element of the `sorted_num` again. (Go back to setp 3)
6. If it cannot be brought forward, check the following elements of the `sorted_num` var.
7. If `k` is zero or all characters are moved to form the smallest number (`num` var is empty string), the repetition statement ends.
8. If all the strings of `num` var are not moved to `answer` var (`k` == 0), paste the remaining `num` string after `answer` string.  
   <br/><br/>

## 3. Solution

### [C++]

```c++
class Solution {
public:
    string minInteger(string num, int k) {
        string answer = "";
        int i = 0;

        string sorted_num = num;
        sort(sorted_num.begin(), sorted_num.end());

        while(k && num != "") {
            if (num.find(sorted_num[i]) <= k) {
                k -= num.find(sorted_num[i]);
                answer += sorted_num[i];
                num.erase(num.find(sorted_num[i]), 1);
                sorted_num.erase(i, 1);
                i = -1;
            }
            i++;
        }

        answer += num;

        return answer;
    }
};
```

<br/><br/>

## 4. To Think Deeper

- I checked the test case that didn't pass, and it was a timeout, so is the algorithm itself correct?
- I think the algorithm is simple and well-organized
  <br/><br/><br/>

## 5. Reference ٩( ᐛ )و

- [C++ official doc] std:string:erase <https://www.cplusplus.com/reference/string/string/erase/>
  > - Use `erase()` to erase a string, first parameter is starting point of erasing and second is number of erasing

<br/><br/><br/>

```
출처: LeetCode Contest, https://leetcode.com/contest/
```
