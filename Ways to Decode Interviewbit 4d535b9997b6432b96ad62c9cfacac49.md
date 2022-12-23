# Ways to Decode | Interviewbit

Created: August 9, 2022 12:14 PM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/ways-to-decode/

**Problem Description**

A message containing letters from A-Z is being encoded to numbers using the following mapping:

```
 'A' -> 1
 'B' -> 2
 ...
 'Z' -> 26

```

Given an encoded message **A** containing digits, determine the total number of ways to decode it modulo **109 + 7**.

**Problem Constraints**

**Input Format**

The first and the only argument is a string **A**.

**Output Format**

Return a single integer denoting the total number of ways to decode it modulo **109 + 7**.

**Example Input**

Input 1:

```
 A = "8"

```

Input 2:

```
 A = "12"

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 Given encoded message "8", it could be decoded as only "H" (8).
 The number of ways decoding "8" is 1.

```

Explanation 2:

```
 Given encoded message "12", it could be decoded as "AB" (1, 2) or "L" (12).
 The number of ways decoding "12" is 2.

```

```cpp
int helper(string &s,vector<int>&dp,int index)
{
    int mod=pow(10,9)+7;
    if(index==s.length())
    {
        return dp[index]=1;
    }
    if(s[index]=='0')
    {
        return dp[index]=0;
    }
    if(dp[index]!=-1)
    {
        return dp[index];
    }
    if(dp[index+1]==-1)
    {
        dp[index+1]=(helper(s,dp,index+1)%mod);
    }
    int res=dp[index+1];
    if(index+1<s.length() && (s[index]=='1' || (s[index]=='2' && s[index+1]<='6')))
    {
        if(dp[index+2]==-1)
        {
            dp[index+2]=(helper(s,dp,index+2)%mod);
        }
        res=(res+dp[index+2])%mod;
    }
    return dp[index]=res;
}
int Solution::numDecodings(string A) 
{
    vector<int>dp(A.length()+1,-1);
    return helper(A,dp,0);
}
```