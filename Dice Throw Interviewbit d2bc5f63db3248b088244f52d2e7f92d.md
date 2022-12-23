# Dice Throw | Interviewbit

Created: August 2, 2022 1:13 AM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/dice-throw/

**Problem Description**

You are given **A** dices with faces numbered from **1** to **B**.
 You have to find out the number of ways to get to sum **C**.

Since, the number can be large, output the answer modulo **109 + 7**.

**Problem Constraints**

**Input Format**

The first argument is the integer A.
 The second argument is the integer B.
 The third argument is the integer C.

**Output Format**

Return a single integer denoting the number of ways to get to the required sum modulo 109 + 7.

**Example Input**

Input 1:

```
A = 2
B = 4
C = 5

```

Input 2:

```
A = 2
B = 4
C = 1

```

**Example Output**

Output 1:

```
4

```

Output 2:

```
0

```

**Example Explanation**

Explanation 1:

```
There are 4 different ways to arrange the dices - [1, 4], [2, 3], [3, 2], [4, 1].
```

Explanation 2:

```
Since, the dices are numbered from 1. 2 dices will have the minimum sum of 2.
Therefore, there are zero ways to get to sum 1.

```

```cpp
int Solution::findDiceSum(int A, int B, int C) {
    long dp[A + 1][C + 1];
    long mod = (long) 1e9 + 7;
    for (int i = 0; i <= A; i++)
        for (int j = 0; j <= C; j++)
            dp[i][j] = 0;
    dp[0][0] = 1;
    for (int i = 1; i <= A; i++) {
        for (int j = i; j <= C; j++) {
            dp[i][j] = (dp[i][j - 1] + dp[i - 1][j - 1]) % mod;
            if (j - B - 1 >= 0)
                dp[i][j] = (dp[i][j] - dp[i - 1][j - B - 1] + mod) % mod;
            
        }
    }
    return (int) dp[A][C];
}
```