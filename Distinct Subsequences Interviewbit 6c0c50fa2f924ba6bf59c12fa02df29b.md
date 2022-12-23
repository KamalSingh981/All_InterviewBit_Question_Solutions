# Distinct Subsequences | Interviewbit

Created: August 5, 2022 11:07 PM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/distinct-subsequences/

Given two sequences **A**, **B**, count number of unique ways in sequence **A**, to form a subsequence that is identical to the sequence **B**.

**Subsequence :** A subsequence of a string is a new string which is formed from the original string by deleting some (can be none) of the characters without disturbing the relative positions of the remaining characters. (ie, “ACE” is a subsequence of “ABCDE” while “AEC” is not).

**Input Format:**

```
The first argument of input contains a string, A.
The second argument of input contains a string, B.

```

**Output Format:**

```
Return an integer representing the answer as described in the problem statement.

```

**Constraints:**

```
1 <= length(A), length(B) <= 700

```

**Example :**

```
Input 1:
    A = "abc"
    B = "abc"

Output 1:
    1

Explanation 1:
    Both the strings are equal.

Input 2:
    A = "rabbbit"
    B = "rabbit"

Output 2:
    3

Explanation 2:
    These are the possible removals of characters:
        => A = "ra_bbit"
        => A = "rab_bit"
        => A = "rabb_it"

    Note: "_" marks the removed character.

```

```cpp
int ans(string &A, string &B, int i, int j, int &n, int &m, vector<vector<int>> &dp){
    if(j == m) return 1;
    if(i == n) return 0;
    
    if(dp[i][j] != -1) return dp[i][j];
    
    
    if(A[i] == B[j]){
        return dp[i][j] = ans(A, B, i + 1, j +1, n, m, dp) + ans(A, B, i + 1, j, n, m,dp);
    }
    else{
        return dp[i][j] = ans(A, B, i+1, j, n, m,dp);
    }
}

int Solution::numDistinct(string A, string B) {
    int n = A.size();
    int m = B.size();
    
    
    vector<vector<int>> dp(n, vector<int>(m, -1));
    return ans(A, B, 0, 0, n, m, dp);
}
```

Bottom Up Approach

```cpp
int Solution::numDistinct(string A, string B) {
    int m = A.size();
    int n = B.size();
    
    
    vector<vector<int>> dp(n + 1, vector<int>(m + 1, 0));
    
    for(int i = 0; i<m + 1; i++){
        dp[0][i] = 1;
    }
    
    for(int i = 1; i<n + 1; i++){
        for(int j = 1; j<m +1; j++){
            if(B[i-1 ] == A[j -1]){
                dp[i][j] = dp[i-1][j-1] + dp[i][j-1];
            }
            else{
                dp[i][j] = dp[i][j-1];
            }
            
        }
    }
    
    return dp[n][m];
    
}
```