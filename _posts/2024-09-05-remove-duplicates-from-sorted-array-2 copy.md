---
title: LeetCode | 80. Remove Duplicates from Sorted Array 2
author: serin
date: 2024-09-05 19:46:00 +0900
categories: [Algorithm, Leetcode]
tags: [Medium, Array, TwoPointers]
image:
  path: /assets/img/Algorithm/2024/09/05/main.png
  alt: main
---

## [Remove Duplicates from Sorted Array 2](https://leetcode.com/problems/remove-duplicates-from-sorted-array-ii/description)

Given an integer array `nums` sorted in **non-decreasing order**, remove some duplicates **in-place** such that each unique element appears **at most twice**. The relative order of the elements should be kept the **same**.

Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the **first part** of the array `nums`. More formally, if there are `k` elements after removing the duplicates, then the first `k` elements of `nums` should hold the final result. It does not matter what you leave beyond the first `k` elements.

Return `k` *after placing the final result in the first `k` slots of `nums`*.

Do **not** allocate extra space for another array. You must do this by **modifying the input array in-place** with O(1) extra memory.


### 🗝️ 문제 이해
1. 주어진 배열에서 중복을 제거한다.
   1. 단, 각 유니크 요소가 최대 2번까지만 나타나도록 한다.
   2. 중복이 제거된 최종 배열의 길이를 k로 반환한다.
2. 문제 요구 사항
   1. in-place 알고리즘을 사용해야 한다.
   2. 공간 복잡도는 O(1) 추가 메모리만 사용해야 한다.

> Input: nums = [1,1,1,2,2,3]  
> Output: 5, nums = [1,1,2,2,3,_]

> Input: nums = [0,0,1,1,1,1,2,3,3]  
> Output: 7, nums = [0,0,1,1,2,3,3,_,_]


### ✨ 접근 방법

> Two Pointer 기법을 사용하여 인덱스별 값과 주어진 값을 비교해 나가자.
{: .prompt-tip }

유니크 값이 1개가 아닌 최대 2개까지 허용된 문제이다.  
이전 세트 문제와 상황은 동일하고, 조건이 추가되었으므로 초기 조건들이 수정되면 될 것으로 예상하였다.

1. 배열을 순회하며
   1. `k` 에 기존 값과 다를 때에 값을 증가시킨다.
   2. 배열의 인덱스는 계속 나아가며 nums[k]와 값을 비교해 나간다. 
2. 단, 2번째 요소까지는 유일성이 보장되므로 k=2 부터 시작하면 된다.

![example](/assets/img/Algorithm/2024/09/05/example.jpeg){: .w-75 .normal}

### 🔥 풀이 코드

```kotlin
class Solution {
    fun removeDuplicates(nums: IntArray): Int {
        if (nums.size <= 2) return nums.size
        
        var k = 2
        for (i in 2 until nums.size) {
            if (nums[i] != nums[k - 2]) {
                nums[k] = nums[i]
                k++
            }
        }
        return k
    }
}
```

위 문제를 제출했을 때, 코드를 거의 수정하지 않고 냈더니 생각보다 느렸다! (왜지... 이전 문제는 이렇게까지 느리지 않았다.)

![result](/assets/img/Algorithm/2024/09/05/result.png)

우선 풀이 방법 자체를 아얘 변경하기 보다는 그 안에서 최대한 최적화할 수 있도록 이것저것 시도해 보았다.  
1. `nums[i] != nums[k-2]`
   1. 해당 비교 조건을 `nums[i] > nums[k-2]` 로 변경
   2. 주어진 배열은 어차피 정렬되어 있으므로 현재 요소가 두 칸 앞의 요소보다 크다면 반드시 새로운 요소이다.
2. `nums[k] = nums[i]`, `k++`
   1. `nums[k++] = nums[i]` 로 합쳤다.
   2. 검색해보니 후위 증가 연산자는 배열 안에도 들어갈 수 있는 것이었다! 미세하게나마 영향을 주지 않을까 싶어 적용해 보았다.

```kotlin
class Solution {
    fun removeDuplicates(nums: IntArray): Int {
      if (nums.size <= 2) return nums.size
      
      var k = 2
      for (i in 2 until nums.size) {
          if (nums[i] > nums[k - 2]) {
              nums[k++] = nums[i]
          }
      }
      return k
  }
}
```

![result](/assets/img/Algorithm/2024/09/05/result2.png)

그 결과 살짝 중상위권으로 진입할 수 있었다! 👏 완벽하게 최적화는 아니지만, 조금씩 앞으로 나가는 고민들을 해 보았다.

### 🙆‍♀️ 배우게 된 점

- 메모리 사용 제한이 들어간 문제의 경우, 효율성에 대해서 잘 고려해봐야 한다.
