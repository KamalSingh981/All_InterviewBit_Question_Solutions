# Min Sum Path in Triangle | Interviewbit

Created: August 2, 2022 9:21 PM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/min-sum-path-in-triangle/

Given a triangle, find the minimum path sum from top to bottom. Each step you may move to adjacent numbers on the row below.

For example, given the following triangle

```
[
     [2],
    [3,4],
   [6,5,7],
  [4,1,8,3]
]

```

The minimum path sum from top to bottom is `11` (i.e., `2 + 3 + 5 + 1 = 11`).

> 
> 
> 
> **Note:** Bonus point if you are able to do this using only O(n) extra space, where n is the total number of rows in the triangle.
> 

```cpp
int Solution::minimumTotal(vector<vector<int> > &A) {
    // Do not write main() function.
    // Do not read input, instead use the arguments to the function.
    // Do not print the output, instead return values as specified
    // Still have a doubt. Checkout www.interviewbit.com/pages/sample_codes/ for more details
    
    int n = A.size();
    int m = A[0].size();
    
    
    for(int i = 1; i<n; i++){
        for(int j = 0; j<A[i].size(); j++){
            if(j == 0){
                A[i][j] += A[i -1][j];
            }
            else if(j < A[i].size()- 1){
                A[i][j] += min(A[i-1][j-1], A[i-1][j]);
            }
            else{
                A[i][j] += A[i-1][j-1];
            }
        }
    }
    
    int ans = INT_MAX;
    for(int i = 0; i<A[n-1].size(); i++){
        ans = min(A[n-1][i], ans);
    }
    return ans; 
}
```

Using O(n) Space 

```cpp
int Solution::minimumTotal(vector<vector<int> > &A) {
    // Do not write main() function.
    // Do not read input, instead use the arguments to the function.
    // Do not print the output, instead return values as specified
    // Still have a doubt. Checkout www.interviewbit.com/pages/sample_codes/ for more details
    int n=A.size(),sz=A[n-1].size(),col;
    vector <int> dp(sz,0);
    for(int j=0;j<A[n-1].size();j++)
    dp[j]=A[n-1][j];
    for(int i=n-2;i>=0;i--){
        for(int j=0;j<A[i].size();j++){
            col=j;
            dp[col]=min(dp[col],dp[col+1])+A[i][j];
        }
    }
    return dp[0];
}
```