# Dice Rolls | Interviewbit

Created: July 31, 2022 3:07 PM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/dice-rolls/

**Problem Description**

You rolled a dice **K** times and got a sum of **A** after summing all the values you got after a roll.
Find the number of ways you could have got a sum of **A** after rolling **K** times, since this value can be very large return **modulo** **109+7**.

**Problem Constraints**

**Input Format**

**Output Format**

**Example Input**

**Example Output**

**Example Explanation**

Explanation 1:

```
Ways to get sum 2 are {1, 1} {2}.

```

Explanation 2:

```
Ways to get sum 3 are {1, 1, 1}, {1, 2}, {2, 1}, {3}

```

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
int Solution::solve(int A) {
    int M = 1000000007;
    int dp[A+1+6] = {0};
    dp[1] = 1;
    dp[2] = 2;
    dp[3] = 4;
    dp[4] = 8;
    dp[5] = 16;
    dp[6] = 32;
    for(int i = 7; i<=A; i++){
        for(int j = 1; j<=6; j++){
            dp[i] = (dp[i] + dp[i-j])%M;
        }
    }
    return dp[A]%M;
}
```