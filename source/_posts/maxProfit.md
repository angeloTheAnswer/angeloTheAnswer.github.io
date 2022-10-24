---
title: maxProfit
top: false
cover: false
toc: true
mathjax: true
date: 2021-09-07 19:17:35
password:
summary: 上升区间求和
tags:
- python
- Solution
- Array
categories:
- Solution
---

**题目:**
**给你一个整数数组 prices ，其中 prices[i] 表示某支股票第 i 天的价格。**
**在每一天，你可以决定是否购买和/或出售股票。你在任何时候 最多 只能持有 一股 股票。你也可以先购买，然后在 同一天 出售。**
**返回 你能获得的 最大 利润 。**

*思路：*
*交易者初始状态是持币未持股，所以一定是先买在卖，既然是先买在卖，那么要想收益，一定是后一日的股价大于前一日的股价*
*题意是求上升区间的高度和*

```sh
class Solution:
    def maxProfit(self, prices: List[int]) -> int:
        if len(prices) < 2:
            return 0
        sum = 0 
        for i in range(0,len(prices)-1):
            if prices[i+1] - prices[i]>0:
                temp = prices[i+1] - prices[i]
                sum+=temp
        return sum
```

**边界说明：**
<code>len(prices) < 2</code>
*因为买、卖后才能获利，所以prices的长度小于2无法获利*
<code>range(0,len(prices)-1)</code>
*由于要比较后一天i+1与当前一天的价格i,因此i+1要小于prices的长度*

**TheAnswer**
*运算符<code>+=</code>表示将运算符左边变量的内容与运算符右边变量的内容相加，并再次将结果存储到运算符左边的变量中*

