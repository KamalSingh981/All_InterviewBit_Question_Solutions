# Longest Arithmetic Progression | Interviewbit

Created: August 5, 2022 3:33 AM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/longest-arithmetic-progression/

Find **longest** Arithmetic Progression in an integer array **A** of size **N**, and return its length.

More formally, find longest sequence of indices, **0 < i1 < i2 < … < ik < ArraySize(0-indexed)** such that sequence **A[i1], A[i2], …, A[ik]** is an Arithmetic Progression.

Arithmetic Progression is a sequence in which all the differences between consecutive pairs are the same, i.e sequence **B[0], B[1], B[2], …, B[m - 1]** of length **m** is an Arithmetic Progression if and only if **B[1] - B[0] == B[2] - B[1] == B[3] - B[2] == … == B[m - 1] - B[m - 2]**

**Note:** The common difference can be positive, negative or 0.

**Input Format:**

```
The first and the only argument of input contains an integer array, A.

```

**Output Format:**

```
Return an integer, representing the length of the longest possible arithmetic progression.

```

**Constraints:**

```
1 <= N <= 1000
1 <= A[i] <= 1e9

```

**Examples:**

```
Input 1:
    A = [3, 6, 9, 12]

Output 1:
    4

Explanation 1:
    [3, 6, 9, 12] form an arithmetic progression.

Input 2:
    A = [9, 4, 7, 2, 10]

Output 2:
    3

Explanation 2:
    [4, 7, 10] form an arithmetic progression.

```

```cpp
int Solution::solve(const vector<int> &a) {
    unordered_map<int, int> mp;
    int n = a.size();
    if(n <=2)
    return n;
    int dp[1001][1001];
    int maxi = 2;
    for(int i=0; i<n-1; i++)
    {
        for(int j = i+1; j<n; j++)
        {
            dp[i][j] = 2;
            int need = 2*a[i] - a[j];
            if(mp.find(need)!=mp.end())
            {
                dp[i][j] = max(dp[i][j], 1 + dp[mp[need]][i]);
                maxi = max(maxi, dp[i][j]);
            }
        }
        mp[a[i]] = i;
    }
    return maxi;
}
```