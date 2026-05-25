# Buy-and-sell-stocks-k-transactions

You are given an integer array prices where prices[i] is the price of a given stock on the ith day, and an integer k.
Find the maximum profit you can achieve. You may complete at most k transactions: i. e. you may buy at most k times and sell at most k times.
Note: You may not engage in multiple transactions simultaneously (i. e., you must sell the stock before you buy again).

Input
You don't need to read inputs or print anything. Complete the function maxProfit() that takes an integer representing k and an array prices and returns an integer representing the maximum profit you can achieve.

Custom Input:
The first line of input contains elements of "prices" separated by space.
The second line of input contains k

Constraints
1 ≤ k ≤ 100
1 ≤ prices. length ≤ 1000
0 ≤ prices[i] ≤ 1000
Output
Return the maximum profit you can achieve.
Example
Input:
3 2 6 5 0 3
2
Output:
7
Explanation:
Buy on day 2 (price = 2) and sell on day 3 (price = 6), profit = 6-2 = 4.
Then buy on day 5 (price = 0) and sell on day 6 (price = 3), profit = 3-0 = 3.
Total profit 4+3 = 7.

def maxProfit(k, prices):
    n = len(prices)
    if n == 0:
        return 0

    # If k is large → unlimited transactions case
    if k >= n // 2:
        profit = 0
        for i in range(1, n):
            if prices[i] > prices[i - 1]:
                profit += prices[i] - prices[i - 1]
        return profit

    dp = [[0, 0] for _ in range(k + 1)]

    # initialize holding state
    for t in range(1, k + 1):
        dp[t][1] = -prices[0]

    for i in range(1, n):
        for t in range(1, k + 1):
            dp[t][0] = max(dp[t][0], dp[t][1] + prices[i])
            dp[t][1] = max(dp[t][1], dp[t - 1][0] - prices[i])

    return dp[k][0]
