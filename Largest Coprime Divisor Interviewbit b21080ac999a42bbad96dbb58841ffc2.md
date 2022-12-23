# Largest Coprime Divisor | Interviewbit

Created: May 21, 2022 11:28 PM
Tags: Math
URL: https://www.interviewbit.com/problems/largest-coprime-divisor/

**Problem Description**

You are given two positive numbers A and B. You need to find the maximum valued integer X such that:

**X** divides A i.e. **A % X = 0X** and **B** are co-prime i.e. **gcd(X, B) = 1**
For example,

A = 30
B = 12
We return
X = 5

**Problem Constraints**

**Input Format**

**Output Format**

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```python
int primefactor(int A, int B){
    int c = 2;
    while(__gcd(A, B)!=1){
        if(A%c == 0 && B%c == 0){
            A /= c;
        }
        else{
            c++;
        }
    }
    return A;
}

int Solution::cpFact(int A, int B) {
    return primefactor(A, B);

}
```