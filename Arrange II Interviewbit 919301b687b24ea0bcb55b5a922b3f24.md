# Arrange II | Interviewbit

Created: August 2, 2022 3:34 AM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/arrange-ii/

You are given a sequence of black and white horses, and a set of K stables numbered 1 to K. You have to accommodate the horses into the stables in such a way that the following **conditions are satisfied:**

> 
> 
> - You fill the horses into the stables preserving the relative order of horses. For instance, you cannot put horse 1 into stable 2 and horse 2 into stable 1. You have to preserve the ordering of the horses.
> - No stable should be empty and no horse should be left unaccommodated.
> - Take the product (`number of white horses * number of black horses`) for each stable and take the sum of all these products. This value should be the minimum among all possible accommodation arrangements

**Example:**

```

Input: {WWWB} , K = 2
Output: 0

Explanation:
We have 3 choices {W, WWB}, {WW, WB}, {WWW, B}
for first choice we will get 1*0 + 2*1 = 2.
for second choice we will get 2*0 + 1*1 = 1.
for third choice we will get 3*0 + 0*1 = 0.

Of the 3 choices, the third choice is the best option.

```

**If a solution is not possible, then return -1**

```cpp
int Solution::arrange(string A, int B) {
    int n = A.length();
    if(B>n){
        return -1;
    }
    if(B==n){
        return 0;
    }
    vector<vector<int>> dp(n, vector<int>(B, 0));
    int wh = 0, bh = 0;
    for(int  i = 0; i<n; i++){
        if(A[i] == 'W') wh++;
        else bh++;
        dp[i][0] = bh*wh;
    }
    
    for(int j = 1; j<B; j++){
        for(int  i = 0; i<n; i++){
            int wh = 0, bh = 0;
            dp[i][j] = INT_MAX;
            for(int k = i; k>=0; k--){
                if(A[k] == 'W') wh++;
                else bh++;
                dp[i][j] = min(dp[i][j], wh*bh +   ((k-1>=0)?dp[k-1][j-1]:0));
            }
        }
    }
    
    
    return dp[n-1][B-1];
}
```