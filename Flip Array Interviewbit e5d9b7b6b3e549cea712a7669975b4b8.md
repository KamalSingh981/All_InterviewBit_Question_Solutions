# Flip Array | Interviewbit

Created: August 7, 2022 5:34 PM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/flip-array/

Given an array of positive elements, you have to flip the sign of some of its elements such that the resultant sum of the elements of array should be minimum non-negative(as close to zero as possible). Return the minimum no. of elements whose sign needs to be flipped such that the resultant sum is minimum non-negative.

**Constraints:**

```
 1 <= n <= 100

```

Sum of all the elements will not exceed 10,000.

**Example:**

```
A = [15, 10, 6]

```

ans = 1 (Here, we will flip the sign of 15 and the resultant sum will be 1 )

```
A = [14, 10, 4]

```

ans = 1 (Here, we will flip the sign of 14 and the resultant sum will be 0)

> 
> 
> 
> Note that flipping the sign of 10 and 4 also gives the resultant sum 0 but flippings there are not minimum.
> 

```cpp
int Solution::solve(const vector<int> &A) {
    int n = A.size();
    int sums = 0;
    for(auto i:A){
        sums += i;
    }
    int sum = sums/2;
    
    int dp[n+1][sum + 1];
    for(int i= 0; i<=n; i++){
        for(int j = 0; j<=sum; j++){
            if(j == 0) dp[i][j] = 0;
            else if(i == 0) dp[i][j] = (INT_MAX - 1);
            else if(j>= A[i -1]) dp[i][j] = min(1 + dp[i-1][j - A[i-1]], dp[i-1][j]);
            else dp[i][j] = dp[i-1][j];
        }
    }
    while(sum > 0 && dp[n][sum] >= (INT_MAX - 1)){
        sum--;
        
    }
    return dp[n][sum];   
}
```