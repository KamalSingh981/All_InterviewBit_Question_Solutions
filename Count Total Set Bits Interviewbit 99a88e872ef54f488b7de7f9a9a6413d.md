# Count Total Set Bits | Interviewbit

Created: June 15, 2022 7:31 PM
Tags: bit manipullation
URL: https://www.interviewbit.com/problems/count-total-set-bits/

**Problem Description**

Given a positive integer **A**, the task is to count the total number of set bits in the binary representation of all the numbers from **1** to **A**.

Return the count modulo **109 + 7**.

**Problem Constraints**

**Input Format**

First and only argument is an integer **A**.

**Output Format**

Return an integer denoting the ( Total number of set bits in the binary representation of all the numbers from **1** to **A** )modulo **109 + 7**.

**Example Input**

Input 1:

```
 A = 3

```

Input 2:

```
 A = 1

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 DECIMAL    BINARY  SET BIT COUNT
    1          01        1
    2          10        1
    3          11        2
 1 + 1 + 2 = 4
 Answer = 4 % 1000000007 = 4

```

Explanation 2:

```
 A = 1
  DECIMAL    BINARY  SET BIT COUNT
    1          01        1
 Answer = 1 % 1000000007 = 1

```

```python
int setbit(int A){
    if(A == 0) return 0;
    int n = 0;
    long long int ans = 0;
    while(pow(2, n)<=A) n++;
    n--;
    ans = n*pow(2, n-1) + (A-pow(2,n) + 1) + setbit(A-pow(2,n));
    ans = ans%1000000007;
    return ans;
}
int Solution::solve(int A) {
    return setbit(A);
}
```