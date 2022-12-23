# Excel Column Number | Interviewbit

Created: May 14, 2022 1:43 AM
URL: https://www.interviewbit.com/problems/excel-column-number/

**Problem Description**

Given a column title **A** as appears in an Excel sheet, return its corresponding column number.

**Problem Constraints**

**Input Format**

First and only argument is string A.

**Output Format**

**Example Input**

Input 1:

```
 "A"

```

Input 2:

```
 "AB"

```

**Example Output**

Output 1:

```
 1

```

Output 2:

```
 28

```

**Example Explanation**

Explanation 1:

```
 A -> 1

```

Explanation 2:

```
A  -> 1
B -> 2
C -> 3
...
Z -> 26
AA -> 27
AB -> 28

```

```cpp
int Solution::titleToNumber(string A) {
    int d = A.length();
    int ans = 0;
    for(int i = 0; i < d; i++){
        ans *= 26;
        ans += A[i] - 'A' + 1;
    }
    return ans;
}
```