# Divide Integers | Interviewbit

Created: June 16, 2022 12:55 AM
Tags: bit manipullation
URL: https://www.interviewbit.com/problems/divide-integers/

Divide two integers without using multiplication, division and mod operator.

Return the floor of the result of the division.

**Example:**

**Also, consider if there can be overflow cases. For overflow case, return INT_MAX.**

Note: INT_MAX = 2^31 - 1

```python
int Solution::divide(int dividend, int divisor) {
    int sign = 1;
    if (dividend<0){sign = -sign;}
    if (divisor<0){sign = -sign;}
     
    unsigned long long tmp = abs((long long)dividend);
    unsigned long long tmp2 = abs((long long)divisor);
            
    unsigned long c = 1;
    while (tmp2 < tmp){
        tmp2 = tmp2<<1;    
        c = c<<1;
    }
     
    long long res = 0;
    while (tmp>=abs((long long)divisor)){
        while (tmp2 <= tmp){
            tmp -= tmp2;
            res = res+c;
        }
        tmp2=tmp2>>1;
        c=c>>1;    
    }
     
    return (sign*res >= INT_MAX ||  sign*res < INT_MIN) ? INT_MAX : sign*res;
}
```