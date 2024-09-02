---
title: LeetCode | 88. Merge Sorted Arrys
author: serin
date: 2024-09-02 20:16:00 +0900
categories: [Algorithm, Leetcode]
tags: [Easy]
image:
  path: /assets/img/Algorithm/20240902/main.png
  alt: main
---

## [Merge Sorted Arrys](https://leetcode.com/problems/merge-sorted-array/description)

You are given two integer arrays `nums1` and `nums2`, sorted in **non-decreasing** order, and two integers `m` and `n`, representing the number of elements in `nums1` and `nums2` respectively.

**Merge** `nums1` and `nums2` into a single array sorted in **non-decreasing order.**

The final sorted array should not be returned by the function, but instead be *stored inside the array* `nums1`. To accommodate this, `nums1` has a length of `m + n`, where the first `m` elements denote the elements that should be merged, and the last `n` elements are set to `0` and should be ignored. `nums2` has a length of `n`.


### 🗝️ 문제 이해
1. 목표는 주어진 2개의 정수 배열 `nums1`, `nums2`를 병합하여 하나의 정렬된 배열을 만드는 것이다.
2. 주어진 것
   1. 비감소 순서 정렬 정수 배열 2개 `nums1`, `nums2`
   2. 각각의 크기 `m`, `n`

### ✨ 접근 방법

> Two Pointer 기법을 사용하여 선형 자료 구조를 탐색하자.
> {: .prompt-tip }

주어진 예시를 보면, nums1의 길이는 이미 nums2와의 길이 합으로 이루어져 있고, 긴 나머지 부분은 0으로 채워져 있는 것을 볼 수 있다.  
뒤 쪽 인덱스부터 높은 순서로 값을 비교해나가며 채워 넣으려는 아이디어에서 시작되었다.

1. 각 배열의 마지막 유효한 값의 인덱스의 값을 저장할 포인터를 생성한다. (p1, p2)
   1. 최종 nums1의 인덱스 값을 저장할 포인터도 생성하여 하나씩 비교해 나간다.
2. `nums1[p1]`, `nums2[p2]` 를 비교하여 더 큰 값을 `nums1[p]`에 넣는다.
3. `nums2`의 모든 요소가 처리되면 종료한다.
   1. 즉, 0보다 작아지면 종료한다.

> nums1 = [1,2,3,0,0,0], nums2 = [2,5,6]  
>   p1=2, p2=2, p=5 ➡️ nums1[2] < nums2[2] ➡️ nums1 = [1,2,3,0,0,6]  
>   p1=2, p2=1, p=4 ➡️ nums1[2] < nums2[1] ➡️ nums1 = [1,2,3,0,5,6]  
>   p1=2, p2=0, p=3 ➡️ nums1[2] > nums2[0] ➡️ nums1 = [1,2,3,3,5,6]  
>   p1=1, p2=0, p=2 ➡️ nums1[1] = nums2[0] ➡️ nums1 = [1,2,2,3,5,6]  

### 🔥 풀이 코드

```kotlin
class Solution {
    fun merge(nums1: IntArray, m: Int, nums2: IntArray, n: Int): Unit {
        var p1 = m - 1
        var p2 = n - 1
        var p = m + n -1

        while (p2 >= 0) {
            if (p1 >= 0 && nums1[p1] > nums2[p2]) {
                nums1[p] = nums1[p1]
                p1--
            } else {
                nums1[p] = nums2[p2]
                p2--
            }
            p--
        }
    }
}
```

![result](/assets/img/Algorithm/20240902/result.png)

### 🙆‍♀️ 배우게 된 점

- 처음에는 당연하게 앞에서부터 비교하는 것을 생각했는데, 풀이를 진행하다 보니 비어있는 배열의 끝부분부터 넣으면 더 효율적이겠다는 생각을 하게 되었다.
  - 배열에 여유 공간(0으로 채워진 부분)이 있으면 최대한 활용하자. 로직이 단순해진다.
- 큰 값부터 채워나가면 각 요소를 한 번만 이동시키면 된다.
