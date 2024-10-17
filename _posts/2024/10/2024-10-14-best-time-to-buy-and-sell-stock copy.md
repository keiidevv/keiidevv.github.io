---
title: LeetCode | 121. Best Time to Buy and Sell Stock
author: serin
date: 2024-10-14 19:23:00 +0900
categories: [Algorithm, Leetcode]
tags: [Easy, Array, Dynamic Programming]
image:
  path: /assets/img/Algorithm/2024/10/14/main.png
  alt: main
---

## [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description)

You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

You want to maximize your profit by choosing a **single day** to buy one stock and choosing a **different day in the future** to sell that stock.

Return the *maximum profit you can achieve from this transaction*. If you cannot achieve any profit, return `0`.

### 🗝️ 문제 이해
1. 주식 거래에서 최대 이익을 찾는 것이 목표!
   1. [이익 = 미래의 날에 판 금액 - 현재 산 금액] 의 최대값을 계산해야 한다.
   2. 즉, 가장 싸게 사서 가장 비싸게 팔아야 한다.

> Example 1:  
> Input: prices = [7,1,5,3,6,4]  
> Output: 5  
> Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.  
> Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.  


> Example 2:  
> Input: prices = [7,6,4,3,1]  
> Output: 0  
> Explanation: In this case, no transactions are done and the max profit = 0.  

### ✨ 접근 방법

배열을 순회하며 현재 금액이 최소 금액보다 작으면 계속 기록하고, 현재 가격 대비 최대 이익값을 계산해 나간다.

1. 빈 배열을 우선적으로 체크한다.
2. `minPrice` 변수를 두고, 배열을 순회하며 현재 가격이 `minPrice`보다 작으면 업데이트한다.
   1. 그렇지 않으면, 현재 가격과 `minPrice` 의 차이를 계산하여 `maxProfix` 값을 비교해 나간다.
   2. 계산한 값이 현재의 `maxProfit` 보다 크면, `maxProfix`을 저장한다.
3. 최종적으로 배열 순회를 모두 마치고 `maxProfix` 을 반환한다.


### 🔥 풀이 코드

```kotlin
class Solution {
    fun maxProfit(prices: IntArray): Int {
        if (prices.isEmpty()) return 0
        
        var minPrice = Int.MAX_VALUE // 초기값 세팅
        var maxProfit = 0
        
        for (price in prices) {
            if (price < minPrice) {
                minPrice = price
            } else {
                // 현재 최대값과 비교된 최대값을 중, 더 큰 값을 저장한다.
                maxProfit = maxOf(maxProfit, price - minPrice)
            }
        }
        
        return maxProfit
    }
}
```

![result](/assets/img/Algorithm/2024/10/14/result.png)

### 🙆‍♀️ 배우게 된 점

- 단 한번의 순회로 문제를 해결할 수 있으므로 O(n)의 시간 복잡도를 가지고 있다.
- 또한, 추가 공간을 사용하지 않았으므로 O(1)의 공간 복잡도를 가지고 있다.
