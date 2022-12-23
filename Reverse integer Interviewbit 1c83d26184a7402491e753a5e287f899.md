# Reverse integer | Interviewbit

Created: May 14, 2022 12:50 AM
URL: https://www.interviewbit.com/problems/reverse-integer/

**Problem Description**

You are given an integer **N** and the task is to reverse the digits of the given integer. Return **0** if the result overflows and does not fit in a 32 bit signed integer

Look at the example for clarification.

**Problem Constraints**

N belongs to the Integer limits.

**Input Format**

**Output Format**

Return a single integer denoting the reverse of the given integer.

**Example Input**

Input 1:

```
 x = 123
```

Input 2:

```
 x = -123
```

**Example Output**

Output 1:

```
 321

```

Ouput 2:

```
 -321
```

**Example Explanation**

```
 If the given integer is negative like -123 the output is also negative -321.
```

```cpp
int reversDigits(int num) {
     
    int rev = 0  ;
     
    while(num != 0){        
        int rem = num % 10 ;
        num /= 10 ;
         
        if(rev > INT_MAX/10 || rev == INT_MAX/10 && rem > 7){
            return 0 ;
        }
         
        if(rev < INT_MIN/10 || rev == INT_MIN/10 && rem < -8){
            return 0 ;
        }
         
        rev = rev*10 + rem ;
    }
     
    return rev ;
     
}
```