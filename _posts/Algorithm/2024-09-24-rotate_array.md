---
title: LeetCode | 189. Rotate Array
author: serin
date: 2024-09-24 21:19:00 +0900
categories: [Algorithm, Leetcode]
tags: [Medium, Array, TwoPointers]
image:
  path: /assets/img/Algorithm/2024/09/24/main.png
  alt: main
---

## [Rotate Array](https://leetcode.com/problems/rotate-array/description)

Given an integer `array` nums, rotate the array to the right by `k` steps, where `k` is non-negative.

### 🗝️ 문제 이해
1. 주어진 양수인 k 만큼 배열을 뒤집고, 결과를 리턴한다.

> Input: nums = [1,2,3,4,5,6,7], k = 3
> Output: [5,6,7,1,2,3,4]
> Explanation:
> rotate 1 steps to the right: [7,1,2,3,4,5,6]
> rotate 2 steps to the right: [6,7,1,2,3,4,5]
> rotate 3 steps to the right: [5,6,7,1,2,3,4]
> Example 2:

> Input: nums = [-1,-100,3,99], k = 2
> Output: [3,99,-1,-100]
> Explanation: 
> rotate 1 steps to the right: [99,-1,-100,3]
> rotate 2 steps to the right: [3,99,-1,-100]

### ✨ 접근 방법

주어진 `k` 만큼 배열을 뒤로 밀어야 한다. 가장 간단한 방법은 당연히 `k`번 그대로 미는 것..이지만 더 효율적인 방법을 찾아야겠지..!  
이 문제를 처음 고민했을 때에는 `in-place` 로 가장 최적의 방법을 찾기 어려워서 배열 순환을 다시 검색했다.  

1. `k` 개를 기준으로 덩어리를 2개로 나눈다.
2. 덩어리 안에서 각각 배열을 뒤집는다.
   1. 덩어리 1 뒤집기, 덩어리 2 뒤집기
3. 전체 배열을 다시 뒤집는다.
   1. 해당 부분에서 뒤집혔던 덩어리 배열이 다시 돌아오고, 전체적인 덩어리 순서는 바뀌게 된다!
   2. (이 부분을 새로 고안해내기에는 어려웠다. 😢)

![example](/assets/img/Algorithm/2024/09/24/example.jpeg){: .w-75 .normal}


### 🔥 풀이 코드

```kotlin
class Solution {
    fun rotate(nums: IntArray, k: Int) {
        val n = nums.size
        val effectiveK = k % n
        
        reverse(nums, 0, n - 1)
        reverse(nums, 0, effectiveK - 1)
        reverse(nums, effectiveK, n - 1)
    }

    fun reverse(nums: IntArray, start: Int, end: Int) {
        var left = start
        var right = end
        while (left < right) {
            val temp = nums[left]
            nums[left] = nums[right]
            nums[right] = temp
            left++
            right--
        }
    }
}
```

![result](/assets/img/Algorithm/2024/09/24/result.png)

### 🙆‍♀️ 배우게 된 점

- 배열의 대칭성
  - 각 배열은 오른쪽으로 돌리나, 왼쪽으로 돌리나 동일한 습성을 가지고 있다.
  - 실제로 직접 example을 손으로 그렸을 때에는 오른쪽으로 돌렸는데, 코드는 왼쪽으로 돌려도 무방했다. (k 덩어리를 어디로 나누느냐의 차이)
- 배열 순환의 특성
  - 끝과 시작이 연결되어 있다고 생각하니 더 이해하기 쉬웠다.
