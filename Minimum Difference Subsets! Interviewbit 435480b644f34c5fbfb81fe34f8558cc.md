# Minimum Difference Subsets! | Interviewbit

Created: August 2, 2022 5:11 PM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/minimum-difference-subsets/

**Problem Description**

Given an integer array **A** containing **N** integers.

You need to divide the array **A** into two subsets S1 and S2 such that the absolute difference between their sums is minimum.

Find and return this **minimum possible absolute difference**.

**NOTE:**

- Subsets can contain elements from A in any order (not necessary to be contiguous).
- Each element of A should belong to any one subset S1 or S2, not both.
- It may be possible that one subset remains empty.

**Problem Constraints**

**Input Format**

First and only argument is an integer array **A**.

**Output Format**

Return an integer denoting the minimum possible difference among the sums of two subsets.

**Example Input**

**Example Output**

**Example Explanation**

Explanation 1:

```
 Subset1 = {1, 5, 6}, sum of Subset1 = 12
 Subset2 = {11}, sum of Subset2 = 11

```

```cpp
int minSubsetSumDifference(vector < int > & arr, int n) {
  int totSum = 0;

  for (int i = 0; i < n; i++) {
    totSum += arr[i];
  }

  vector < vector < bool >> dp(n, vector < bool > (totSum + 1, false));

  for (int i = 0; i < n; i++) {
    dp[i][0] = true;
  }

  if (arr[0] <= totSum)
    dp[0][arr[0]] = true;

  for (int ind = 1; ind < n; ind++) {
    for (int target = 1; target <= totSum; target++) {

      bool notTaken = dp[ind - 1][target];

      bool taken = false;
      if (arr[ind] <= target)
        taken = dp[ind - 1][target - arr[ind]];

      dp[ind][target] = notTaken || taken;
    }
  }

  int mini = 1e9;
  for (int i = 0; i <= totSum; i++) {
    if (dp[n - 1][i] == true) {
      int diff = abs(i - (totSum - i));
      mini = min(mini, diff);
    }
  }
  return mini;
}

int Solution::solve(vector<int> &A) {
    return minSubsetSumDifference(A, A.size());
    
}
```