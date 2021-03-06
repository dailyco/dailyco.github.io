---
title: "LeetCode Weekly Contest 196 : Can Make Arithmetic Progression From Sequence"
date: 2020-07-11
author: YuJin Kim
categories: [Problem Solving, Leetcode, Weekly Contest]
tags: [leetcode, coding test, easy, algorithm, sorting, c++]
sitemap:
  changefreq: daily
---

Because it was the first time to solve a problem presented in English when studying algorithms, besides the competition, I was a little embarrassed. However the problem was short and the examples were out, so I wasn't really tired. It was a little hard to figure out the problem by just looking for words that I didn't know... Well, I think it is okay because I can study English while solving the algorithm problem | ᐕ)੭\*⁾⁾  
<br/>
<br/>

## 1. Problem

Given an array of numbers arr.  
A sequence of numbers is called an arithmetic progression if the difference between any two consecutive elements is the same.

Return true if the array can be rearranged to form an arithmetic progression, otherwise, return false.  
<br/>

**Example1 :**

> **Input:** arr = [3,5,1]  
> **Output:** true  
> **Explanation:** We can reorder the elements as [1,3,5] or [5,3,1] with differences 2 and -2 respectively, between each consecutive elements.

<br/>
**Example2 :**  
> **Input:** arr = [1,2,4]  
> **Output:** false  
> **Explanation:** There is no way to reorder the elements to obtain an arithmetic progression.

<br/>

### Constraints

- 2 <= arr.length <= 1000
- 10^6 <= arr[i] <= 10^6
  <br/><br/><br/>

## 2. Thinking Algorithm

1. Sort the `arr` received by parameter in ascending order.
2. Find the difference between the first and second elements of arr. (This value is tolerance unit)
3. Start with the second element of `arr` and check if the next element increases in tolerance unit.
4. If it does not increase in tolerance unit, return `false`.
5. When all elements are increased in tolerance unit, the repeating statement (for loop) ends and returns `true`.  
   <br/><br/>

## 3. Solution

### [C++]

```c++
class Solution {
public:
    bool canMakeArithmeticProgression(vector<int>& arr) {
        sort(arr.begin(), arr.end());

        int diff = arr[1] - arr[0];
        for(int i = 1; i < arr.size() - 1; i++) {
            if (arr[i+1] - arr[i] != diff) return false;
        }

        return true;
    }
};
```

<br/><br/>

## 4. To Think Deeper

- The point is that sorting arr at first.
  <br/><br/><br/>

## 5. Reference ٩( ᐛ )و

- Nothing ¯＼_(ツ)_/¯

<br/><br/><br/>

```
출처: LeetCode Contest, https://leetcode.com/contest/
```
