# Number of Sundays | Interviewbit

Created: May 10, 2022 10:52 AM
URL: https://www.interviewbit.com/problems/number-of-sundays/

**Problem Description**

Given the start day of the month A and number of days in the month B, find number of sundays in the month.

**Problem Constraints**

**Input Format**

**Output Format**

**Example Input**

Input 1:

```
A = "Sunday"
B = 1

```

Input 2:

```
A = "Monday"
B = 14

```

**Example Output**

**Example Explanation**

Explanation 1:

```
The only day in the month is sunday.
```

Explanation 2:

```
The 7th and 14th day of the month will be sunday
```

```cpp
int Solution::solve(string A, int B) {
    if(A=="Monday"){
        return (B)/7;
    }
    else if(A=="Tuesday"){
        return (B+1)/7;
    }
    else if(A=="Wednesday"){
        return (B+2)/7;
    }
    else if(A=="Thursday"){
        return (B+3)/7;
    }
    else if(A=="Friday"){
        return (B+4)/7;
    }
    else if(A=="Saturday"){
        return (B+5)/7;
    }
    else if(A=="Sunday"){
        return (B+6)/7;
    }
}
```