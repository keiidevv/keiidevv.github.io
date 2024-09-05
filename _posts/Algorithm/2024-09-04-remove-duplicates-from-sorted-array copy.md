---
title: LeetCode | 26. Remove Duplicates from Sorted Array
author: serin
date: 2024-09-04 19:57:00 +0900
categories: [Algorithm, Leetcode]
tags: [Easy, Array, TwoPointers]
image:
  path: /assets/img/Algorithm/20240904/main.png
  alt: main
---

## [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description)

Given an integer array `nums` sorted in **non-decreasing order**, remove the duplicates **in-place** such that each unique element appears only **once**. The **relative order** of the elements should be kept the **same**. Then return the number of unique elements in `nums`.

Consider the number of unique elements of `nums` to be `k`, to get accepted, you need to do the following things:

- Change the array `nums` such that the first `k` elements of `nums` contain the unique elements in the order they were present in `nums` initially. The remaining elements of `nums` are not important as well as the size of `nums`.
- Return `k`.


### 🗝️ 문제 이해
1. 주어진 배열에 `val` 과 중복된 숫자가 있다면
   1. 배열에서 제외하고,
   2. 최종 유일한 수의 개수를 `k` 로 반환한다. -> 목표!
2. 문제 요구 사항
   1. `in-place` 로 수정하기
   2. 상대적 순서를 유지하기
   3. 결과인 `k` 를 반환하기

> Input: nums = [1,1,2]  
> Output: 2, nums = [1,2,_]

>Input: nums = [0,0,1,1,1,2,2,3,3,4]  
> Output: 5, nums = [0,1,2,3,4,_,_,_,_,_]

### ✨ 접근 방법

> Two Pointer 기법을 사용하여 인덱스별 값과 주어진 값을 비교해 나가자.
{: .prompt-tip }

27번 문제를 먼저 풀었는데.. 이 문제가 나에겐 조금 더 복잡했다.  
처음에 든 아이디어는, 해당 배열은 굳이 뒤에서부터 비교해나갈 필요가 없고, 앞에서부터 중복이 아닌 값들을 체크해서 유니크 값들로만 채워나가면 될 것 같다.

1. 배열을 순회하며
   1. `k` 에 기존 값과 다를 때에 값을 증가시킨다.
   2. 배열의 인덱스는 계속 나아가며 nums[k]와 값을 비교해 나간다. 
2. `i` 가 배열 끝까지 도달하면 `k` 값을 리턴한다.

뭔가 머리속으로는 알 것 같은데, 실제 동작하는 코드를 어떻게 짤지가 고민되어서 아래처럼 직접 긴 예시를 가지고 동작을 손으로 확인해 보았다.  
`k` 는 유니크한 값을 세는 역할도 하고, `i` 의 값을 비교해줄 인덱스 역할도 할 수 있다. 이렇게 중복값을 제거하며 배열에 반영해 나가면 `in-place` 요구사항을 만족시키면서 메모리를 효율적으로 사용할 수 있다.

![example](/assets/img/Algorithm/20240904/example.jpeg){: .w-75 .normal}

### 🔥 풀이 코드

```kotlin
class Solution {
    fun removeDuplicates(nums: IntArray): Int {
        // 엣지 케이스 추가
        if (nums.isEmpty()) return 0

        var k = 1
        for (i in 1 until nums.size) { // 최초 인덱스 0은 유일한 값임을 고려, until 가독성 고려
            if (nums[i] != nums[k - 1]) {
                nums[k] = nums[i]
                k++
            }
        }

        return k
    }
}
```

이렇게 진행할 경우의 공간 복잡도는 O(1) 이다.  
추가로, 알고리즘만 반영했을 때에는 결과가 느려서 빈 배열 케이스를 추가하는 조건을 넣었더니 살짝 빨라졌다!

![result](/assets/img/Algorithm/20240904/result.png)

### 🙆‍♀️ 배우게 된 점

- 단일 배열에서 두 개의 포인터를 사용하여 효율적으로 비교하며 값을 확인해나갈 수 있다.
- 비정렬 배열이 아닌, 정렬 배열에서는 천천히 앞에서부터 비교해 나가면 된다.
- 빈 배열 확인과 같은 엣지 케이스를 고려하는 것 또한 알고리즘 효율성에 기여될 수 있다.
  - 기존에는 문제 풀기에 바빠 고려하지 못했지만, 앞으로 여유가 된다면 추가로 고민해 보려고 한다.
- 코드 가독성에 대한 고민
  - 반복문을 작성할 때, `for(i in 1..nums.size - 1)` 로 작성한 것을
  - `for(i in 1 until nums.size)` 로 수정하였다.
  - 개인적으로 코드를 작성할 때에는 처음 시도한 반복문이 더 편했으나, `until` 을 사용하는 것이 코틀린에서 더 관용적이며 가독성이 좋다고 생각되어 수정하였다. 이 부분에 대해서는 내 개인적인 생각이니 다른 코드들을 참고해 가며 확인해봐야 할 것 같다.
