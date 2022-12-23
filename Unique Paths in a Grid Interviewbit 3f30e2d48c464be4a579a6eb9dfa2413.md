# Unique Paths in a Grid | Interviewbit

Created: August 2, 2022 1:34 AM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/unique-paths-in-a-grid/

Given a grid of size m * n, lets assume you are starting at `(1,1)` and your goal is to reach `(m,n)`. At any instance, if you are on `(x,y)`, you can either go to `(x, y + 1)` or `(x + 1, y)`.

Now consider if some obstacles are added to the grids. How many unique paths would there be?
 An obstacle and empty space is marked as 1 and 0 respectively in the grid.

**Example :**
 There is one obstacle in the middle of a 3x3 grid as illustrated below.

```
[
  [0,0,0],
  [0,1,0],
  [0,0,0]
]

```

The total number of unique paths is `2`.

> 
> 
> 
> **Note:** m and n will be at most 100.
> 

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
int Solution::uniquePathsWithObstacles(vector<vector<int> > &A) {
    int n = A.size();
    int m = A[0].size();
    for(int  i= 0; i<n; i++){
        for(int j = 0; j<m; j++){
            if(A[i][j] == 1){
                A[i][j] = -1;
            }
        }
    }
    
    
    for(int i = 0; i<m; i++){
        if(A[0][i] == -1){
            break;
        }
        else{
            A[0][i] = 1;
        }
    }
    for(int i = 0; i<n; i++){
        if(A[i][0] == -1){
            break;
        }
        else{
            A[i][0] = 1;
        }
    }
    
    for(int i = 1; i<n; i++){
        for(int  j = 1; j<m; j++){
            if(A[i][j] == -1){
                continue;
            }
            if(A[i][j-1] != -1) A[i][j] += A[i][j-1];
            if(A[i-1][j] != -1) A[i][j] += A[i-1][j];
        }
    }
    if(A[n-1][m-1] == -1){
        return 0;
    }
    return A[n-1][m-1]; 
}
```