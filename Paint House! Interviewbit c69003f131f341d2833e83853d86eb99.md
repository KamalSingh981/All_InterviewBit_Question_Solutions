# Paint House! | Interviewbit

Created: August 1, 2022 3:41 AM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/paint-house/

**Problem Description**

There are a row of **N** houses, each house can be painted with one of the three colors: **red, blue or green.**

The cost of painting each house with a certain color is different. You have to paint all the houses such that no two adjacent houses have the same color.

The cost of painting each house with a certain color is represented by a `N x 3` cost matrix **A**.

For example, **A[0][0]** is the cost of painting house 0 with color red; **A[1][2]** is the cost of painting house 1 with color green, and so on.

Find the **minimum total cost** to paint all houses.

**Problem Constraints**

1 <= N <= 105

1 <= A[i][j] <= 103

**Input Format**

First and only argument is an 2D integer matrix **A** of size `N x 3` denoting the cost to paint the houses.

**Output Format**

Return an integer denoting the **minimum total cost** to paint all houses.

**Example Input**

Input 1:

**Example Output**

**Example Explanation**

Explanation 1:

```
 Paint house 1 with red and house 2 with green i.e A[0][0] + A[1][1] = 1 + 11 = 12

```

```cpp
int Solution::solve(vector<vector<int> > &A) {
    
    int n = A.size();
    vector<vector<int>> dp(A.size(), vector<int>(3, 0));
    dp[0][0] = A[0][0];
    dp[0][1] = A[0][1];
    dp[0][2] = A[0][2];
    for(int i = 1; i<A.size(); i++){
        dp[i][0] = A[i][0] + min(dp[i-1][1], dp[i - 1][2]);
        dp[i][1] = A[i][1] + min(dp[i-1][0], dp[i - 1][2]);
        dp[i][2] = A[i][2] + min(dp[i-1][1], dp[i - 1][0]);
        
    }
    
    return min(min(dp[n-1][0], dp[n-1][1]), dp[n-1][2]);
}
```