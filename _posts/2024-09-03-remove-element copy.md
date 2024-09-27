---
title: LeetCode | 27. Remove Element
author: serin
date: 2024-09-03 19:41:00 +0900
categories: [Algorithm, Leetcode]
tags: [Easy, Array, TwoPointers]
image:
  path: /assets/img/Algorithm/2024/09/03/main.png
  alt: main
---

## [Remove Element](https://leetcode.com/problems/remove-element/description)

Given an integer array `nums` and an integer `val`, remove all occurrences of `val` in `nums` **in-place**. The order of the elements may be changed. Then return the number of elements in `nums` which are not equal to `val`.

Consider the number of elements in `nums` which are not equal to `val` be `k`, to get accepted, you need to do the following things:

- Change the array `nums` such that the first `k` elements of nums contain the elements which are not equal to `val`. The remaining elements of `nums` are not important as well as the size of `nums`.
- Return `k`.


### 🗝️ 문제 이해
1. 주어진 배열에 `val` 과 같은 숫자가 있다면
   1. 배열에서 제외하고,
   2. 같지 않은 수를 `k` 로 반환한다. -> 목표!

> Input: nums = [3,2,2,3], val = 3  
> Output: 2, nums = [2,2,_,_]

> Input: nums = [0,1,2,2,3,0,4,2], val = 2  
> Output: 5, nums = [0,1,4,0,3,_,_,_]

### ✨ 접근 방법

> Two Pointer 기법을 사용하여 인덱스별 값과 주어진 값을 비교해 나가자.
{: .prompt-tip }

Two pointer 기법은 리스트에 순차적으로 접근해야 할 때, 두 개의 점위치를 기록하면서 처리하는 알고리즘이다. 특히 정렬 리스트, 병합 정렬에 매우 유용하다.  

해당 문제의 경우 배열을 순회하면서 주어진 값과 다른 값을 조건으로 확인해 나가면 될 것으로 예상된다.

1. 배열을 순회하며
   1. `val` 값과 동일하지 않으면 해당 자리에 같지 않은 수를 대체한다.
   2. `k` 값을 증가시켜 다음 인덱스로 이동한다.
2. 순회가 끝나면 `k` 값을 리턴한다.

실제 동작하는 예시를 통해서 어떻게 구해 나갈지를 고민해 보았다. 아래와 같이 동작할 것을 예상하고 풀이 코드를 작성하였다.

![example](/assets/img/Algorithm/2024/09/03/example.jpeg){: .w-75 .normal}

### 🔥 풀이 코드

```kotlin
class Solution {
    fun removeElement(nums: IntArray, `val`: Int): Int {
        var k = 0
        for (i in nums.indices) {
            if (nums[i] != `val`) {
                nums[k] = nums[i]
                k++
            }
        }
        return k
    }
}
```

막상 작성하니 매우 간단한 코드!

![result](/assets/img/Algorithm/2024/09/03/result.png)

### 🙆‍♀️ 배우게 된 점

- 확실히 직접 동작을 그리면서 하니 코드를 짜기 수월하였다.
- Two pointer는 배열 문제에서 매우매우 유용하다! 
