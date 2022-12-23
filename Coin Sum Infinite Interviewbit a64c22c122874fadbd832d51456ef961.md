# Coin Sum Infinite | Interviewbit

Created: August 1, 2022 9:59 PM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/coin-sum-infinite/

You are given a set of coins **S**. In how many ways can you make sum **N** assuming you have infinite amount of each coin in the set.

**Note :** Coins in set **S** will be unique. Expected space complexity of this problem is **O(N)**.

**Example :**

**Note that the answer can overflow. So, give us the answer % 1000007**

```cpp
int Solution::coinchange2(vector<int> &A, int B) {
    
    vector<int> dp(B + 1, 0);
    dp[0] = 1;
    
    for(int i = 0; i<A.size(); i++){
        for(int j = A[i]; j <= B; j++){
            dp[j] += dp[j - A[i]];
            dp[j] %= 1000007;
        }
    }
    return dp[B];
    
}
```

In efficient solution

```cpp
int findchange(vector<int> &A, int n, int size, vector<vector<int>> &dp){
    if(n == 0){
        return 1;
    }
    if(n<0){
        return 0;
    }
    if(size <=0 and n >= 1){
        return 0;
    }
    
    // Look up
    if(dp[n][size - 1] != -1){
        return dp[n][size - 1];
    }
     
    return dp[n][size - 1] = (findchange(A, n, size -1, dp)% 1000007 + findchange(A, n - A[size -1], size, dp)% 1000007)% 1000007;
}

int Solution::coinchange2(vector<int> &A, int B) {
    
    vector<vector<int>> dp(B + 1, vector<int>(A.size(), -1));
    return findchange(A, B, A.size(), dp);
}
```