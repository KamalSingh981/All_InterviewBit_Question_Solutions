# Palindromic Time | Interviewbit

Created: May 9, 2022 4:35 PM
URL: https://www.interviewbit.com/problems/palindromic-time/

**Problem Description**

Given a string **A** which represents a time in **24 hour HH:MM** format.
Find the minimum number of minutes need to pass to reach **palindromic time**.
Let some time be **XY:ZW** then it is palindromic if **X == W** and **Y == Z**.

**Problem Constraints**

**Input Format**

**Output Format**

**Example Input**

**Example Output**

**Example Explanation**

Explanation 1:

```
After 1 minute time will be 00:00 which is a palindromic time.

```

Explanation 2:

```
After 12 minute time will be 21:12 which is a palindromic time.

```

```cpp
int Solution::solve(string A) {
    int min = 0;
    int hr = (A[0]-48)*10 + A[1]-48;
    int mm = (A[3]-48)*10 + A[4]-48;
    while(hr/10 !=mm%10 || hr%10 != mm/10){
        mm++;
        if(mm>59){
            mm = 0;
            hr++;
        }
        if(hr>23){
            hr = 0;
        }
        min++;
    }
    return min;
}
```