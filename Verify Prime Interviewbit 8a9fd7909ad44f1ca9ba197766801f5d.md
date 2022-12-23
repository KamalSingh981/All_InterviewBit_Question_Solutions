# Verify Prime | Interviewbit

Created: May 12, 2022 12:22 AM
URL: https://www.interviewbit.com/problems/verify-prime/

Given a number N, verify if N is prime or not.

Return 1 if N is prime, else return 0.

**Example :**

**Problem Approach:**

VIDEO : https://www.youtube.com/watch?v=7VPA-HjjUmU

Complete code in the hint.

```cpp
int Solution::isPrime(int A) {
    if(A==1) return 0;
    for(int i=2 ; i*i<=A ; i++)
        if(A%i==0) return 0;
    return 1;
}
```