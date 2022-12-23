# Climbing Stairs | Interviewbit

Created: May 10, 2022 1:25 AM
URL: https://www.interviewbit.com/problems/climbing-stairs/

**Problem Description**

Given an integer array **A** of length **N**. Where **A**i is the cost of stepping on the **ith** stair.
From **ith** stair, you can go to **i+1th** or **i+2th** numbered stair.
Initially, you are at **1st** stair find the minimum cost to reach **Nth** stair.

**Problem Constraints**

**Input Format**

**Output Format**

**Example Input**

**Example Output**

**Example Explanation**

```cpp
int Solution::solve(vector<int> &A) {
   int d[A.size()];
    d[0]=A[0];
    d[1]=A[0]+A[1];
    for(int i=2;i<A.size();i++)
    {
        d[i]=A[i]+min(d[i-1],d[i-2]);
    }

    return d[A.size()-1];
}
```