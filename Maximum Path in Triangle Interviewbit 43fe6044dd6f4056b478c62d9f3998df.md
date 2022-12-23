# Maximum Path in Triangle | Interviewbit

Created: August 2, 2022 2:43 AM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/maximum-path-in-triangle/

**Problem Description**

Given a 2D integer array **A** of size  `N * N`  representing a triangle of numbers.

Find the maximum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

**NOTE:**

- Adjacent cells to cell (i,j) are only (i+1,j) and (i+1,j+1)
- Row i contains i integer and n-i zeroes for all i in [1,n] where zeroes represents empty cells.

**Problem Constraints**

0 <= N <= 1000

0 <= A[i][j] <= 1000

**Input Format**

First and only argument is an 2D integer array **A** of size `N * N`.

**Output Format**

Return a single integer denoting the maximum path sum from top to bottom in the triangle.

**Example Input**

Input 1:

```
 A = [
        [3, 0, 0, 0]
        [7, 4, 0, 0]
        [2, 4, 6, 0]
        [8, 5, 9, 3]
     ]

```

Input 2:

```
 A = [
        [8, 0, 0, 0]
        [4, 4, 0, 0]
        [2, 2, 6, 0]
        [1, 1, 1, 1]
     ]

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 Given triangle looks like:  3
                             7 4
                             2 4 6
                             8 5 9 3
        So max path is (3 + 7 + 4 + 9) = 23

```

Explanation 1:

```
 Given triangle looks like:  8
                             4 4
                             2 2 6
                             1 1 1 1
        So max path is (8 + 4 + 6 + 1) = 19

```

```cpp
// recursive solution
int pathSum(int i,int j,vector<vector<int>> &A, vector<vector<int>> &dp)
{
    if(i == A.size() || j == A.size()){
        return 0;
    }
    
    // Look Up
    if(dp[i][j] != -1 ){
       return dp[i][j];
    }
    
    
    return dp[i][j] = A[i][j] + max(pathSum(i +1, j, A, dp), pathSum(i +1, j + 1, A, dp));
}

int Solution::solve(vector<vector<int> > &A) {
    
    
    // iterative solution
    vector<vector<int>> dp(A.size(), vector<int>(A.size() ,0));
    dp[0][0] = A[0][0];
    for(int i = 1; i<A.size(); i++){
        for(int j = 0; j<i + 1; j++){
            if(j!= 0){
                dp[i][j] = A[i][j] + max(dp[i-1][j], dp[i-1][j-1]);
            }else{
                dp[i][j] = A[i][j] + dp[i-1][j];
            }
        }
    }
    int ans = 0;
    for(int i=0; i<A.size(); i++){
        ans = max(dp[A.size() -1][i],ans);
    }
    

    return ans;
}
```