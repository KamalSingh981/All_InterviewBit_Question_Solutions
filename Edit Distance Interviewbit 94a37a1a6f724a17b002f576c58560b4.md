# Edit Distance | Interviewbit

Created: August 5, 2022 5:44 PM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/edit-distance/

Given two strings **A** and **B**, find the minimum number of steps required to convert **A** to **B**. (each operation is counted as 1 step.)

You have the following 3 operations permitted on a word:

- Insert a character
- Delete a character
- Replace a character

**Input Format:**

```
The first argument of input contains a string, A.
The second argument of input contains a string, B.

```

**Output Format:**

```
Return an integer, representing the minimum number of steps required.

```

**Constraints:**

```
1 <= length(A), length(B) <= 450

```

**Examples:**

```
Input 1:
    A = "abad"
    B = "abac"

Output 1:
    1

Explanation 1:
    Operation 1: Replace d with c.

Input 2:
    A = "Anshuman"
    B = "Antihuman"

Output 2:
    2

Explanation 2:
    => Operation 1: Replace s with t.
    => Operation 2: Insert i.

```

```cpp
int Solution::minDistance(string A, string B) {
    
    
    vector<vector<int>> dp(B.size() + 1, vector<int> (A.size() + 1, 0));
    for(int i = 0; i<A.size() + 1; i++){
        dp[0][i] = i;
    }
    for(int i = 0; i<B.size() + 1; i++){
        dp[i][0] = i;
    }
    
    for(int i  = 1 ;i <B.size() + 1; i++){
        for(int j = 1; j<A.size() + 1; j++){
            if(B[i - 1] == A[j-1]){
                dp[i][j] = dp[i-1][j-1]; // if two elements are equal then take the previous digonal value
            }
            else{
                // if two elements are not equal then take the minimum value from left up and diagonal and add 1 to it.
                dp[i][j] = min(min(dp[i-1][j], dp[i][j-1]), dp[i-1][j-1]) +1;
            }
        }
    }
    return dp[B.size()][A.size()]; // return the answer
}
```