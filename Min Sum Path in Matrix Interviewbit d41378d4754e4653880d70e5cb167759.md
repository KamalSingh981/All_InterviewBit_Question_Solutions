# Min Sum Path in Matrix | Interviewbit

Created: May 24, 2022 3:38 PM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/min-sum-path-in-matrix/

**Problem Description**

Given a 2D integer array **A** of size `M x N`, you need to find a path from top left to bottom right which minimizes the sum of all numbers along its path.

**NOTE:** You can only move either down or right at any point in time.

**Input Format**

First and only argument is an 2D integer array **A** of size `M x N`.

**Output Format**

Return a single integer denoting the minimum sum of a path from cell (1, 1) to cell (M, N).

**Example Input**

Input 1:

```
 A = [  [1, 3, 2]
        [4, 3, 1]
        [5, 6, 1]
     ]

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 The path is 1 -> 3 -> 2 -> 1 -> 1
 So ( 1 + 3 + 2 + 1 + 1) = 8

```

```cpp
int Solution::minPathSum(vector<vector<int> > &A) {
    int r = A.size();
    int c = A[0].size() ;
    
    vector<vector<int>> DP(r , vector<int> (c));
    DP[0][0] = A[0][0];

    for(int i = 1; i<c; i++){
        DP[0][i] = DP[0][i-1] + A[0][i];
    }

    for(int j = 1; j<r; j++){
        DP[j][0] = DP[j-1][0] + A[j][0];
    }

    for(int i=1; i<r; i++){
        for(int j = 1; j<c; j++){
            DP[i][j] = A[i][j]  + min(DP[i][j-1], DP[i-1][j]);
        }
    }

    return DP[r-1][c-1];
}
```

## Algorithm

This question uses the concept of dynamic programming.

Let DP[i][j] store the minimum sum of numbers along the path from top left to (i,j).

Basically, DP[i][j] = A[i][j] + min(DP[i-1][j],DP[i][j-1]).

We just need the find the cumulative sum of the first row and column and then we are set to go.