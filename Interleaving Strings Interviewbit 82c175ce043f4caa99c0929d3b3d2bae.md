# Interleaving Strings | Interviewbit

Created: August 10, 2022 1:06 AM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/interleaving-strings/

Given **A**, **B**, **C**, find whether **C** is formed by the interleaving of **A** and **B**.

**Input Format:***

```
The first argument of input contains a string, A.
The second argument of input contains a string, B.
The third argument of input contains a string, C.

```

**Output Format:**

```
Return an integer, 0 or 1:
    => 0 : False
    => 1 : True

```

**Constraints:**

```
1 <= length(A), length(B), length(C) <= 150

```

**Examples:**

```
Input 1:
    A = "aabcc"
    B = "dbbca"
    C = "aadbbcbcac"

Output 1:
    1

Explanation 1:
    "aa" (from A) + "dbbc" (from B) + "bc" (from A) + "a" (from B) + "c" (from A)

Input 2:
    A = "aabcc"
    B = "dbbca"
    C = "aadbbbaccc"

Output 2:
    0

Explanation 2:
    It is not possible to get C by interleaving A and B.

```

```cpp
#include <map>
bool findMyAnswer(string &A, string &B, string &C, int i, int j, map<pair<int, int>, bool> &dp){
    if(i == A.length() and j == B.length()) return true;
    
    if(dp.find({i,j})!=dp.end()) return dp[{i,j}];
    
    
    if(i<A.length() and A[i] == C[i + j] and findMyAnswer(A, B, C, i+1, j, dp)){
        return dp[{i,j}] = true;
    }
    if(j<B.length() and B[j] == C[i + j] and findMyAnswer(A, B, C, i ,j +1, dp)){
        return dp[{i,j}] = true;
    }
    
    dp[{i, j}] = false;
    return false;
}

int Solution::isInterleave(string A, string B, string C) {
    int n = A.length();
    int m = B.length();
    int q = C.length();
    
    if(n + m != q) return false;
    map<pair<int, int>, bool> mp;
    
    return findMyAnswer(A, B, C, 0,0,  mp);
}
```

Bottom Up Approach

```cpp
int Solution::isInterleave(string A, string B, string C) {
    int n = A.length();
    int m = B.length();
    int q = C.length();
    
    if(n + m != q) return false;
    
    vector<vector<int>> dp(n+1, vector<int> (m+1, 0));
    dp[n][m] = 1;
    
    for(int i = n; i>= 0; i--){
        for(int j = m; j>= 0; j--){
            if(i<n and A[i] == C[i + j] and dp[i + 1][j]){
                dp[i][j] = 1;
            }
            if(j <m and B[j] == C[i + j] and dp[i][j + 1]){
                dp[i][j] = 1;
            }
        }
    }
    
    
    return dp[0][0];
}
```