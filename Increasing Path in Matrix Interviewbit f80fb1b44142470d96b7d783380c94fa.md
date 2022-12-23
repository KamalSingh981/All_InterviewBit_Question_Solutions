# Increasing Path in Matrix | Interviewbit

Created: August 2, 2022 1:58 AM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/increasing-path-in-matrix/

**Problem Description**

Given a 2D integer matrix **A** of size **`N x M`**.

From **A[i][j]** you can move to **A[i+1][j]**, if **A[i+1][j]** > **A[i][j]**, or can move to **A[i][j+1]** if **A[i][j+1]** > **A[i][j]**.

The task is to find and output the longest path length possible if we start from the cell **(0, 0)** and want to reach cell **(N - 1, M - 1)**.

**NOTE:**

- If there doesn't exist a path return **1**.

**Problem Constraints**

**Input Format**

First and only argument is an 2D integer matrix **A** of size `N x M`.

**Output Format**

Return a single integer denoting the length of longest path in the matrix if no such path exists return **-1**.

**Example Input**

Input 1:

```
 A = [  [1, 2]
        [3, 4]
     ]

```

Input 2:

```
 A = [  [1, 2, 3, 4]
        [2, 2, 3, 4]
        [3, 2, 3, 4]
        [4, 5, 6, 7]
     ]

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 Longest path is either 1 2 4 or 1 3 4.

```

Explanation 2:

```
 Longest path is 1 2 3 4 5 6 7.

```

```cpp
int Solution::solve(vector<vector<int> > &A) {
    int n = A.size();
    int m = A[0].size();
    vector<vector<bool>> dp(n, vector<bool>(m, false));
    dp[0][0] = true;
    for(int i = 1; i<n; i++){
        if(A[i][0]> A[i - 1][0]){
            dp[i][0] = true;
        }
        else{
            break;
        }
    }
    
    for(int i = 1; i<m; i++){
        if(A[0][i]> A[0][i - 1]){
            dp[0][i] = true;
        }
        else{
            break;
        }
    }
    for(int i= 1; i<n; i++){
        for(int j = 1; j<m; j++){
            if(A[i-1][j] < A[i][j] and dp[i - 1][j] == true){
                dp[i][j] = true;
            }
            if(A[i][j-1] < A[i][j] and dp[i][j-1] == true){
                dp[i][j] = true;
            }
        }    
    }
    if(dp[n-1][m-1] == false){
        return -1;
    }
    return m + n -1;
}
```