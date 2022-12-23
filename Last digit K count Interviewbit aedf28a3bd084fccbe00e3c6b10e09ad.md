# Last digit K count | Interviewbit

Created: May 10, 2022 4:49 PM
URL: https://www.interviewbit.com/problems/last-digit-k-count/

**Problem Description**

Find the number of integers in range **[A, B]** with last digit **C**.

**Problem Constraints**

**Input Format**

**Output Format**

**Example Input**

Input 1:

```
A = 11, B = 111, C = 1

```

Input 2:

```
A = 1, B = 9, C = 0

```

**Example Output**

**Example Explanation**

Explanation 1:

```
The integers are 11, 21, 31, 41, 51, 61, 71, 81, 91, 101, 111

```

Explanation 2:

```
There are no integers in the range with last digit 0.

```

```cpp
int Solution::solve(int A, int B, int C) {
    long long j = A;
    while(j%10!=C and j<B)
    {
        j = j+1;
    }
    int count = 0;
    if(j%10!=C)
    {
        return(count);
    }
    count = (B-j)/10;
    return(count+1);
}
```