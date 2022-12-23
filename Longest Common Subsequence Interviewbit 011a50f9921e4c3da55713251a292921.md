# Longest Common Subsequence | Interviewbit

Created: July 31, 2022 4:27 PM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/longest-common-subsequence/

**Problem Description**

Given two strings **A** and **B**. Find the longest common **sequence** ( A sequence which does not need to be contiguous), which is common in both the strings.

You need to return the length of such longest common subsequence.

**Problem Constraints**

**Input Format**

First argument is an string **A**.

Second argument is an string **B**.

**Output Format**

Return the length of such longest common subsequence between string **A** and string **B**.

**Example Input**

Input 1:

```
 A = "abbcdgf"
 B = "bbadcgf"

```

**Example Output**

**Example Explanation**

```cpp
int Solution::solve(string A, string B) {
    
    int n1 = A.length();
    int n2= B.length();
    
    vector<vector<int>> dp(n1 +1, vector<int>(n2+1, 0));
    
    for(int i = 1; i<= n1; i++){
        for(int j = 1; j<=n2; j++){
            if(A[i - 1] == B[j-1]){
                dp[i][j] = 1 + dp[i-1][j-1];
            }
            else{
                dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
            }
        }
    }
    return dp[n1][n2];
```