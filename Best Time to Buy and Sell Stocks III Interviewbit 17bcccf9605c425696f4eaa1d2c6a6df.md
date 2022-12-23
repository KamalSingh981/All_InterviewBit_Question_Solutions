# Best Time to Buy and Sell Stocks III | Interviewbit

Created: August 8, 2022 1:26 PM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/best-time-to-buy-and-sell-stocks-iii/

Say you have an array, **A**, for which the **ith** element is the price of a given stock on day **i**.

Design an algorithm to find the **maximum** profit. You may complete at most **2** transactions.

Return the maximum possible profit.

**Note:** You may not engage in multiple transactions at the same time (ie, you must sell the stock before you buy again).

**Input Format:**

```
The first and the only argument is an integer array, A.

```

**Output Format:**

```
Return an integer, representing the maximum possible profit.

```

**Constraints:**

```
1 <= length(A) <= 7e5
1 <= A[i] <= 1e7

```

**Examples:**

```cpp
int Solution::maxProfit(const vector<int> &A) {
    
    int n = A.size();
    if(n <= 1) return 0;
    
    vector<vector<int>> dp(3, vector<int>(n, 0));
    
    int ans = 0;
    for(int i = 1; i<=2; i++){
        int var = -A[0] + dp[i-1][0];
        for(int j = 1; j<n; j++){
            dp[i][j] = max(A[j] + var, dp[i][j-1]);
            var = max(var , -A[j] + dp[i-1][j]);
        }
    }
    return dp[2][n-1];
}
```