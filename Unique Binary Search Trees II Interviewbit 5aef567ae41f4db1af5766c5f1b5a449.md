# Unique Binary Search Trees II | Interviewbit

Created: August 7, 2022 4:25 PM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/unique-binary-search-trees-ii/

Given an integer **A**, how many structurally unique BST’s (binary search trees) exist that can store values **1…A**?

**Input Format:**

```
The first and the only argument of input contains the integer, A.

```

**Output Format:**

```
Return an integer, representing the answer asked in problem statement.

```

**Constraints:**

```
1 <= A <= 18

```

**Example:**

```
Input 1:
    A = 3

Output 1:
    5

Explanation 1:

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3

```

```cpp
int Solution::numTrees(int A) {
    int dp[A+1];
    dp[0] = 1;
    for(int i=1;i<=A;i++){
        dp[i]=0;
        for(int j=1;j<=i;j++)
            dp[i] += dp[j-1]*dp[i-j];
    }
    return dp[A];
}
```