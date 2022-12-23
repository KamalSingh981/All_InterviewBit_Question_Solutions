# Word Count | Interviewbit

Created: May 9, 2022 1:55 AM
URL: https://www.interviewbit.com/problems/word-count/

**Problem Description**

Given a string **A**. The string contains some **words separated by spaces**.
Return the **number of words** in the given string.

**Problem Constraints**

**Input Format**

**Output Format**

**Example Input**

Input 1:

```
A = "bonjour"

```

Input 2:

```
A = "hasta la vista"

```

**Example Output**

**Example Explanation**

Explanation 1:

```
The string has only one word "bonjour".
```

Explanation 2:

```
The string have three words "hasta", "la", "vista".
```

```cpp
int Solution::solve(string A) {
    int res=0;
    int n=A.size();
    for(int i=0;i<A.size();i++)
    {
        if(i!=0&&A[i]==' '&&A[i-1]!=' ')
        res++;
    }
    if(A[n-1]!=' ')
    res++;
    return res;
}
```