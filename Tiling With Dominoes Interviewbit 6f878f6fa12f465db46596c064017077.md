# Tiling With Dominoes | Interviewbit

Created: August 8, 2022 2:15 AM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/tiling-with-dominoes/

**Problem Description**

Given an integer **A** you have to find the **number of ways** to fill a `3 x A` board with `2 x 1` dominoes.

Return the answer modulo **109 + 7** .

**NOTE:**

- See the sample explanation for better understanding.

**Problem Constraints**

**Input Format**

First and only argument is an integer **A**.

**Output Format**

Return an integer denoting the **number of ways** to fill a `3 x A` board with `2 x 1` dominoes with modulo **109 + 7**.

**Example Input**

**Example Output**

Output 1:

```
 3

```

Output 2:

```
 0

```

**Example Explanation**

Explanation 1:

```
 Following are all the 3 possible ways to fill up a3 x 2 board.

```

Explanation 2:

```
 Not a even a single way exists to completely fill the grid of size3 x 1.

```

```cpp
int Solution::solve(int A) {
    
    vector<long long int> dp(A+1, 0);
    if(A==1 || A%2==1){
        return 0;
    }
    if(A==2){
        return 3;
    }
    dp[0]  = 1;
    dp[1] = 0;
    dp[2] = 3;
    long long mod = 1e9 + 7;
    for(int i = 3; i<= A; i++){
        if(i%2==1){
            dp[i] = 0;
        }
        else{
            dp[i] = ((dp[i-2]*4)%mod-dp[i-4]+mod)%mod;;
        }
    }
    return dp[A];
}
```