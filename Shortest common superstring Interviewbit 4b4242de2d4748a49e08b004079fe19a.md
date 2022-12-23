# Shortest common superstring | Interviewbit

Created: August 6, 2022 2:45 PM
Tags: Dynamic Programming, Very Hard Question
URL: https://www.interviewbit.com/problems/shortest-common-superstring/

Given a set of strings, **A** of length **N**.

Return the length of smallest string which has all the strings in the set as substring.

**Input Format:**

```
The first and the only argument has an array of strings, A.

```

**Output Format:**

```
Return an integer representing the minimum possible length of the resulting string.

```

**Constraints**:

```
1 <= N <= 18
1 <= A[i] <= 100

```

**Example**:

```
Input 1:
    A = ["aaaa", "aa"]

Output 1:
    4

Explanation 1:
    Shortest string: "aaaa"

Input 2:
    A = ["abcd", "cdef", "fgh", "de"]

Output 2:
    8

Explanation 2:
    Shortest string: "abcdefgh"

```

```cpp
int funct(string A,string B, string& str)
{
    int max=INT_MIN;
    int len1=A.size(),len2=B.size();
    for(int i=1;i<=min(len1,len2);i++)
    {
        if(A.compare(len1-i,i,B,0,i)==0)
        {
            max=i;
            str=A+B.substr(i);
        }
    }
    for(int i=1;i<=min(len1,len2);i++)
    {
        if(A.compare(0,i,B,len2-i,i)==0)
        {
            max=i;
            str=B+A.substr(i);
        }
    }
    return max;
}
int Solution::solve(vector<string> &A) {
    int n=A.size();
    while(n!=1)
    {
        int l,r,maxi=INT_MIN;
        string resstr;
        for(int i=0;i<n;i++)
        {
            for(int j=i+1;j<n;j++)
            {
                string str;
                int res=funct(A[i],A[j],str);
                if(maxi<res)
                {
                    maxi=res;
                    resstr=str;
                    l=i;
                    r=j;
                }
            }
        }
        n--;
        if(maxi==INT_MIN)
        A[0]+=A[n];
        else
        {
            A[l]=resstr;
            A[r]=A[n];
        }
    }
    return A[0].size();
}
```