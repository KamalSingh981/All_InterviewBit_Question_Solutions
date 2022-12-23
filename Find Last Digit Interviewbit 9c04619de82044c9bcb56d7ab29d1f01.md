# Find Last Digit | Interviewbit

Created: May 12, 2022 1:52 AM
URL: https://www.interviewbit.com/problems/find-last-digit/

**Problem Description**

Find last digit of the number AB.
A and B are large numbers given as strings.

**Problem Constraints**

**Input Format**

First argument is a string A.
First argument is a string B.

**Output Format**

**Example Input**

Input 1:

```
A = 2
B = 10

```

Input 2:

```
A = 11
B = 11

```

**Example Output**

**Example Explanation**

```cpp
#include <string>
int mod(string num, int a)
{
    // Initialize result
    int res = 0;
    // One by one process all digits of 'num'
    for (int i = 0; i < num.length(); i++)
        res = (res * 10 + (int)num[i] - '0') % a;
 
    return res;
}
int Solution::solve(string A, string B) {
    int exp = (mod(B, 4) == 0) ? 4 : mod(B,4);
    int res = pow(A[A.size() - 1] - '0', exp);
    return res%10;
  
}
```