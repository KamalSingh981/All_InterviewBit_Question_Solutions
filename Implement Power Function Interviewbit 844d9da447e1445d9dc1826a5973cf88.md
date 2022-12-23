# Implement Power Function | Interviewbit

Created: May 26, 2022 1:14 AM
Tags: Binary Search
URL: https://www.interviewbit.com/problems/implement-power-function/

**Problem Description**

Implement **pow(x, n) % d**.

In other words, given **x**, **n** and **d**,

**find (xn % d)**

Note that remainders on division cannot be negative. In other words, make sure the answer you return is non negative.

**Problem Constraints**

- 10 <= x <= 10 0 <= n <= 10 1 <= d <= 10
    
    9
    
    9
    
    9
    
    9
    

**Example Input**

**Example Output**

**Example Explanation**

```cpp
int Solution::pow(int a, int n, int d) {
    if(a== 0){
        return 0;
    }
    long long ans  = 1, x = a;
    while(n>0){
        if(n&1 ){
            ans = (ans*x)%d;
        }
        n = n>>1;

        x = (x*x)%d;
    }
    return (d+ans)%d;
}
```