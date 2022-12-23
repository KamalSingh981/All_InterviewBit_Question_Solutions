# Merge elements | Interviewbit

Created: July 31, 2022 9:48 PM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/merge-elements/

**Problem Description**

Given an integer array **A** of size **N**. You have to merge all the elements of the array into one with the **minimum possible cost**.

The rule for merging is as follows:

- Choose any two adjacent elements of the array with values say **X** and **Y** and merge them into a single element with value **(X + Y)** paying a total cost of **(X + Y)**.

Return the minimum possible cost of merging all elements.

**Problem Constraints**

1 <= N <= 200

1 <= A[i] <= 103

**Input Format**

First and only argument is an integer array A of size N.

**Output Format**

Return an integer denoting the minimum cost of merging all elements.

**Example Input**

Input 1:

```
 A = [1, 3, 7]
```

Input 2:

```
 A = [1, 2, 3, 4]
```

**Example Output**

Output 1:

```
 15
```

Output 2:

```
 19
```

**Example Explanation**

Explanation 1:

```
 All possible ways of merging:
 a) {1, 3, 7} (cost = 0) -> {4, 7} (cost = 4) -> {11} (cost = 4+11 = 15)
 b) {1, 3, 7} (cost = 0) -> {1, 10} (cost = 10) -> {11} (cost = 10+11 = 21)
 Thus, ans = 15
```

```cpp
int minCost(int i, int j, vector<int> &A, vector<vector<int>> &dp){
    if(i == j) return 0;
    
    if(dp[i][j] != -1){
        return dp[i][j];
    }
    
    int total = 0;
    for(int k = i; k<=j; k++){
        total += A[k];
    }
    int x = INT_MAX;
    for(int k = i + 1; k<=j; k++){
        x = min(x, total + minCost(i, k-1, A, dp) + minCost(k, j, A, dp));
    }
    return dp[i][j] = x;
}

int Solution::solve(vector<int> &A) {
    
    int n = A.size();
    vector<vector<int>> dp(n, vector<int>(n, -1));
    
    return minCost(0,n-1,A, dp);
}
```