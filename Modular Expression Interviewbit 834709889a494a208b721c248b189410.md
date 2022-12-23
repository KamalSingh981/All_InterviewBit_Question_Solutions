# Modular Expression | Interviewbit

Created: July 12, 2022 9:31 PM
Tags: Recursion
URL: https://www.interviewbit.com/problems/modular-expression/

Implement `pow(A, B) % C`.

In other words, given `A`, `B` and `C`, 
 find (AB)%C.

```
Input : A = 2, B = 3, C = 3
Return : 2
2^3 % 3 = 8 % 3 = 2

```

**PROBLEM APPROACH :**

Complete solution in the hint.

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
long long power(int A, int B, int C){
    
    // Base Case
    if(B == 0){
        return 1;
    }
    if(B == 1){
        return A%C;
    }
    
    
    // Recursive Case
    long long mid = power(A, B/2, C)%C;
    
    if(B%2 == 0){
        return (mid*mid)%C;
    }
    return ((mid*mid)%C * (A%C))%C;
}

int Solution::Mod(int A, int B, int C) {
    if(A == 0){
        return 0;
    }
    if(A<0){
        A = (A%C + C)%C;
    }
    return power(A,B,C);
}
```