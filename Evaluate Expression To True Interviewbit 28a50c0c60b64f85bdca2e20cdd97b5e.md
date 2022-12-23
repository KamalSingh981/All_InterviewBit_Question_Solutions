# Evaluate Expression To True | Interviewbit

Created: August 9, 2022 4:01 AM
Tags: Dynamic Programming, Very Hard Question
URL: https://www.interviewbit.com/problems/evaluate-expression-to-true/

Given an expression, **A**, with operands and operators **(OR , AND , XOR)**, in how many ways can you evaluate the expression to true, by grouping in different ways?

Operands are only **true** and **false**.

Return the number of ways to evaluate the expression modulo **103 + 3**.

**Input Format:**

```
The first and the only argument of input will contain a string, A.

The string A, may contain these characters:
    '|' will represent or operator
    '&' will represent and operator
    '^' will represent xor operator
    'T' will represent true operand
    'F' will false

```

**Output:**

```
Return an integer, representing the number of ways to evaluate the string.

```

**Constraints:**

```
1 <= length(A) <= 150

```

**Example:**

```
Input 1:
    A = "T|F"

Output 1:
    1

Explanation 1:
    The only way to evaluate the expression is:
        => (T|F) = T

Input 2:
    A = "T^T^F"

Output 2:
    0

Explanation 2:
    There is no way to evaluate A to a true statement.

```

```cpp
int Solution::cnttrue(string A) {
    int n=A.size();
    int t[n][n],f[n][n],mod=1003;
    memset(t,0,sizeof(t));
    memset(f,0,sizeof(f));
    
    for(int i=0;i<n;i++)
    {
        if(A[i]=='T') t[i][i]=1;
        if(A[i]=='F') f[i][i]=1;
    }
    
    for(int len=3;len<=n;len+=2)
    {
        for(int left=0;left<=n-len;left++)
        {
            int right=left+len-1;
            for(int op=left+1;op<right;op+=2)
            {
                if(A[op]=='^')
                {
                    t[left][right]+=(t[left][op-1]*f[op+1][right]+f[left][op-1]*t[op+1][right])%mod;
                    f[left][right]+=(t[left][op-1]*t[op+1][right]+f[left][op-1]*f[op+1][right])%mod;
                }
                else if(A[op]=='&')
                {
                    t[left][right]+=(t[left][op-1]*t[op+1][right])%mod;
                    f[left][right]+=(t[left][op-1]*f[op+1][right]+f[left][op-1]*t[op+1][right]+f[left][op-1]*f[op+1][right])%mod;
                }
                else if(A[op]=='|')
                {
                    t[left][right]+=(f[left][op-1]*t[op+1][right]+t[left][op-1]*f[op+1][right]+t[left][op-1]*t[op+1][right])%mod;
                    f[left][right]+=(f[left][op-1]*f[op+1][right])%mod;
                }
            }
        }
    }
    
    return t[0][n-1]%mod;
}
```