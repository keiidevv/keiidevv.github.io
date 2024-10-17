---
title: LeetCode | 122. Best Time to Buy and Sell Stock II
author: serin
date: 2024-10-17 19:11:00 +0900
categories: [Algorithm, Leetcode]
tags: [Medium, Dynamic Programming, Greedy]
image:
  path: /assets/img/Algorithm/2024/10/17/main.png
  alt: main
---

## [Best Time to Buy and Sell Stock II](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/description)

You are given an integer array `prices` where `prices[i]` is the price of a given stock on the `ith` day.

On each day, you may decide to buy and/or sell the stock. You can only hold **at most one** share of the stock at any time. However, you can buy it then immediately sell it on the **same day**.

Find and return *the **maximum** profit you can achieve.*

### 🗝️ 문제 이해
1. 이전 문제와 거의 유사하다!
   1. [이익 = 미래의 날에 판 금액 - 현재 산 금액] 의 최대값을 계산해야 한다.
      1. 매일 주식을 사고 팔 수 있다.
      2. 같은 날에도 사고 팔 수 있다.
      3. 한 번에 최대 한 주만 보유할 수 있다.
2. 여러번 사고 파는 경우, 한번에 크게 파는 경우 등 다양한 경우의 수를 생각해볼 수 있다.

> Example 1:  
> Input: prices = [7,1,5,3,6,4]  
> Output: 7   
> Explanation: Buy on day 2 (price = 1) and sell on day 3 (price = 5), profit = 5-1 = 4.  
> Then buy on day 4 (price = 3) and sell on day 5 (price = 6), profit = 6-3 = 3.  
> Total profit is 4 + 3 = 7.  


> Example 2:  
> Input: prices = [1,2,3,4,5]  
> Output: 4  
> Explanation: Buy on day 1 (price = 1) and sell on day 5 (price = 5), profit = 5-1 = 4.  
> Total profit is 4.  


> Example 3:  
> Input: prices = [7,6,4,3,1]  
> Output: 0  
> Explanation: There is no way to make a positive profit, so we never buy the stock to achieve the maximum profit of 0.  

### ✨ 접근 방법

그리디 알고리즘을 활용하여 최대 이익을 계산하는 것이 효율적이다.

1. 배열을 순회하며
   1. 현재 가격이 전날 가격보다 높다면, 그 차이를 `maxProfit`에 더한다. -> 사고 팔았음을 가정하고, 해당 차이만큼 계속 더해줄 수 있다.
   2. 지속적으로 배열이 끝날때까지 진행한다.

![example](/assets/img/Algorithm/2024/10/17/example.jpeg){: .w-75 .normal}

### 🔥 풀이 코드

```kotlin
class Solution {
    fun maxProfit(prices: IntArray): Int {
        var maxProfit = 0
        
        for (i in 1 until prices.size) {
            if (prices[i] > prices[i-1]) {
                maxProfit += prices[i] - prices[i-1]
            }
        }
        
        return maxProfit
    }
}
```

![result](/assets/img/Algorithm/2024/10/17/result.png)

### 🙆‍♀️ 배우게 된 점

- 처음에는 실제로 사고 파는 지점을 모두 지정해야 하는 것을 가정하여 삽질을 하였다. 하지만, 매 순간 최적의 선택을 하는 = 이익이 발생할 때마다 거래를 하는 상황을 가정하니 생각보다 쉽게 풀렸다.
  - 위 조건은 문제의 핵심 조건들을 활용하는 것이 생각보다 많이 중요함을 알려준다.
