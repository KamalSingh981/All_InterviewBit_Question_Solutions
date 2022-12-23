# Subset Sum Problem! | Interviewbit

Created: August 2, 2022 5:21 PM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/subset-sum-problem/

**Problem Description**

Given an integer array **A** of size **N**.

You are also given an integer **B**, you need to find whether their exist a subset in **A** whose sum equal **B**.

If there exist a subset then return **1** else return **0**.

**Problem Constraints**

1 <= N <= 100

1 <= A[i] <= 100

1 <= B <= 105

**Input Format**

First argument is an integer array **A**.

Second argument is an integer **B**.

**Output Format**

Return 1 if there exist a subset with sum **B** else return 0.

**Example Input**

Input 1:

```
 A = [3, 34, 4, 12, 5, 2]
 B = 9

```

Input 2:

```
 A = [3, 34, 4, 12, 5, 2]
 B = 30

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 There is a subset (4, 5) with sum 9.

```

Explanation 2:

```
 There is no subset that add up to 30.

```

```cpp
int Solution::solve(vector<int> &A, int B) {
    
    int n = A.size();
    vector<vector<int>> dp(n, vector<int> (B +1, false));
    
    for(int i = 0; i<n; i++){ // 0 sum is  always possilbe
        dp[i][0] = true;
    }
    
    if(A[0]<=B){
        dp[0][A[0]] = true; // in the first row there will only one cell which is true 
                            // because there is only one element
    }
    
    for(int i = 1; i<n; i++){
        for(int j = 1; j<=B; j++){
            bool previous_val = dp[i -1][j];
            bool if_not_previous;
            if(A[i] <= j){
                if_not_previous = dp[i - 1][j - A[i]];
            }
            dp[i][j] = previous_val || if_not_previous;
        }
    }
    
    return dp[n-1][B];
}
```