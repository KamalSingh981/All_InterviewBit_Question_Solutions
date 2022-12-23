# Repeating Sub-Sequence | Interviewbit

Created: August 5, 2022 10:05 PM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/repeating-subsequence/

**Problem Description**

Given a string **A**, find length of the longest repeating sub-sequence such that the two subsequence don’t have same string character at same position,

i.e., any i’th character in the two subsequences shouldn’t have the same index in the original string.

**NOTE:** Sub-sequence length should be greater than or equal to 2.

**Problem Constraints**

**Input Format**

The first and the only argument of input contains a string **A**.

**Output Format**

Return an integer, 0 or 1:

```
    => 0 : False
    => 1 : True

```

**Example Input**

Input 1:

```
 A = "abab"

```

Input 2:

```
 A = "abba"

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 "ab" is repeated.

```

Explanation 2:

```
 There is no repeating subsequence.

```

```cpp
int Solution::anytwo(string A) {
    
    int n = A.length();
    vector<vector<int>> dp(n, vector<int>(n, 0));
    
    bool flag = false;
    for(int i = 1; i<n; i++){
        if(flag){
            dp[0][i] = 1;
        }
        else if(A[0] == A[i]){
            dp[0][i] = 1;
            flag = true;
        }   
    }
    
    for(int i = 1; i<n; i++){
        for(int j = i + 1; j<n; j++){
            if(A[i] == A[j]){
                dp[i][j] = dp[i-1][j-1] + 1;
            }
            else{
                dp[i][j] = max(max(dp[i-1][j-1], dp[i-1][j]), dp[i][j-1]);
            }
            
            if(dp[i][j]>=2){
                return 1;
            }
        }
    }   
    return 0;
}
```