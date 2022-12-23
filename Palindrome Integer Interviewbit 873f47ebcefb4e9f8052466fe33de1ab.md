# Palindrome Integer | Interviewbit

Created: May 10, 2022 12:29 AM
URL: https://www.interviewbit.com/problems/palindrome-integer/

**Problem Description**

Determine whether an integer is a palindrome. Do this without extra space.

A palindrome integer is an integer x for which reverse(x) = x where reverse(x) is x with its digit reversed. Negative numbers are not palindromic.

**Example** :

```
Input : 12121
Output : 1

Input : 123
Output : 0

```

```cpp
#include <string>
int Solution::isPalindrome(int A) {
    if (A<0){
        return 0;
    }
    int digits = 1;
    int a = A/10;
    while(a!=0){
        a /= 10 ;
        digits *= 10;
    }
    int i = 10;
    while(A!=0){
        int leading = A / digits;
        int trailing = A % 10;
 
        // If first and last digit
        // not same return false
        if (leading != trailing) 
            return 0;
        A = (A % digits) / 10;
        digits = digits / 100;
    }
    return 1;
}
```