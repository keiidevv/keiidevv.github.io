---
title: LeetCode | 169. Majority Element
author: serin
date: 2024-09-07 23:25:00 +0900
categories: [Algorithm, Leetcode]
tags: [Easy, Array, HashTable, ]
image:
  path: /assets/img/Algorithm/20240907/main.png
  alt: main
---

## [Majority Element](https://leetcode.com/problems/majority-element/description)

Given an array `nums` of size `n`, return the *majority* element.

The majority element is the element that appears more than `⌊n / 2⌋` times. You may assume that the majority element always exists in the array.

### 🗝️ 문제 이해
1. 배열을 순회하며 과반수 이상의 숫자를 찾아낸다.

> Input: nums = [3,2,3]  
> Output: 3

> Input: nums = [2,2,1,1,1,2,2]  
> Output: 2

### ✨ 접근 방법

> Boyer Moore 알고리즘을 사용하여 마지막 남은 과반수 요소를 찾아내자.
{: .prompt-tip }

해당 문제에서 사용할 만한 알고리즘으로 보이어 무어 알고리즘이 있다는 것을 알아냈다. 해당 알고리즘에 대한 상세한 공부는 추가 포스팅으로 두고, 해당 문제에서 접근할 방법은 아래와 같다.

1. `candidate` 변수(과반수 후보), `count` 변수(후보의 카운트) 를 저장한다.
   1. 배열을 순회하면서
      1. `count`가 0이면 새로운 후보를 설정
      2. 현재 요소와 후보가 같으면 1을 증가
      3. 현재 요소화 후보가 다르면 1을 감소
   2. 순회가 종료되면 최종적으로 과반수 후보가 남는다.

이와 같이 순회할 경우, 과반수 요소는 무조건 배열의 절반 이상을 차지하므로, 다른 모든 요소들과 짝을 지어도 최소한 하나는 남게 된다.

따라서 마지막에 남는 후보는 반드시 과반수 요소가 된다.

### 🔥 풀이 코드

```kotlin
class Solution {
    fun majorityElement(nums: IntArray): Int {
        var candidate = 0
        var count = 0
        
        for (num in nums) {
            if (count == 0) {
                candidate = num
            }
            count += if (num == candidate) 1 else -1
        }
        
        return candidate
    }
}
```

![result](/assets/img/Algorithm/20240907/result.png)

### 🙆‍♀️ 배우게 된 점

- 보이어 무어 알고리즘
  - 실제 문자열 검색에 사용되는 알고리즘이다.
  - 일반적인 상황에서 문자열은 앞부분보다 뒷부분에서 불일치가 일어날 확률이 높다는 성질을 이용한다.
