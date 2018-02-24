## Best Time to Buy and Sell Stock

```
Say you have an array for which the ith element is the price of a given stock on day i.

If you were only permitted to complete at most one transaction (ie, buy one and sell one share of the stock), design an algorithm to find the maximum profit.

Example 1:
Input: [7, 1, 5, 3, 6, 4]
Output: 5

max. difference = 6-1 = 5 (not 7-1 = 6, as selling price needs to be larger than buying price)
Example 2:
Input: [7, 6, 4, 3, 1]
Output: 0

In this case, no transaction is done, i.e. max profit = 0.

```

一次循环，记录当前最小价格和计算最新的收益，检查是否更新最大收益（一次交易 => 最后的结果由一次减法得到）。

```go
func maxProfit(prices []int) int {
    minPrice, maxProfit, n := 99999, -99999, len(prices)
    for i:=0; i<n; i++ {
        if (prices[i] < minPrice) {
            minPrice = prices[i]
        }
        currentProfit := prices[i] - minPrice
        if (currentProfit > maxProfit) {
            maxProfit = currentProfit
        }
    }
    if(maxProfit > 0) {
        return maxProfit
    }
    return 0
}
```

## Best Time to Buy and Sell Stock II

```
Say you have an array for which the ith element is the price of a given stock on day i.

Design an algorithm to find the maximum profit. You may complete as many transactions as you like (ie, buy one and sell one share of the stock multiple times). However, you may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).
```

多次交易，可能得多次减法的结果累加。

```go

```