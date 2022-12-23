# Greatest Common Divisor | Interviewbit

Created: May 9, 2022 1:57 AM
URL: https://www.interviewbit.com/problems/greatest-common-divisor/

Given 2 non negative integers `m` and `n`, find `gcd(m, n)`

GCD of 2 integers m and n is defined as the greatest integer g such that g is a divisor of both m and n.
 Both `m` and `n` fit in a 32 bit signed integer.

**Example**

```
m : 6
n : 9

GCD(m, n) : 3

```

> 
> 
> 
> **NOTE :** DO NOT USE LIBRARY FUNCTIONS
> 

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
int GCD(int A, int B){
    if(B==0){
        return A;
    }
    else{
        return GCD(B,A%B);
    }
}
int Solution::gcd(int A, int B) {
    if(A>B){
        return GCD(A,B);
    }
    else{
        return GCD(B,A);
    }
}
```