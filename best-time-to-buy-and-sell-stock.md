# Best Time to Buy and Sell Stock 

## Problem Statement

You are given an array `prices` where `prices[i]` is the price of a given stock on the `ith` day. You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.

Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.

## Example 1:

**Input:** prices = [7,1,5,3,6,4]

**Output:** 5

**Explanation:** Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5. Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.

## Example 2:

**Input:** prices = [7,6,4,3,1]

**Output:** 0

**Explanation:** In this case, no transactions are done and the max profit = 0.

## Constraints:

* 1 <= prices.length <= 10^5
* 0 <= prices[i] <= 10^4

## Solution

The solution uses a sliding window technique to find the maximum profit. The window is represented by two pointers `start` and `end`. The `start` pointer represents the buying day and the `end` pointer represents the selling day.

The algorithm iterates through the array and checks if the price at the `end` pointer is greater than the price at the `start` pointer. If it is, the algorithm updates the maximum profit to the maximum of the current profit and the difference between the prices at the `end` and `start` pointers. If the price at the `end` pointer is less than or equal to the price at the `start` pointer, the `start` pointer is moved to the `end` pointer.

The algorithm returns the maximum profit.

## Code

```cpp
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int start = 0;
        int end = 0;
        int maxi = 0;
        while (end < prices.size()) {
            if (prices[end] > prices[start]) {
                maxi = max(maxi, prices[end] - prices[start]);
            } else {
                start = end;
            }
            end++;
        }
        return maxi;
    }
};
```

## Complexity Analysis

* Time Complexity: O(n), where n is the length of the array `prices`.
* Space Complexity: O(1), as the algorithm uses constant space to store the `start` and `end` pointers and the maximum profit.


[Sliding Window: Best Time to Buy and Sell Stock Python](https://youtu.be/1pkOgXD63yU?si=065c2EgGgymzyY4t) 
"The provided solution is implemented in Python. The link is included to facilitate a better understanding of the problem."

[LeetCode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/)