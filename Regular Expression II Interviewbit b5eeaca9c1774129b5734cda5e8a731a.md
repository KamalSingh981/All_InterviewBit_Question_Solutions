# Regular Expression II | Interviewbit

Created: August 10, 2022 12:28 AM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/regular-expression-ii/

Implement regular expression matching with support for `'.'` and `'*'`.

`'.'` Matches any single character.`'*'` Matches zero or more of the preceding element.

The matching should cover the entire input string (not partial).

The function prototype should be:

```
int isMatch(const char *s, const char *p)

```

Some examples:

```
isMatch("aa","a") → 0
isMatch("aa","aa") → 1
isMatch("aaa","aa") → 0
isMatch("aa", "a*") → 1
isMatch("aa", ".*") → 1
isMatch("ab", ".*") → 1
isMatch("aab", "c*a*b") → 1

```

Return `0 / 1` ( 0 for false, 1 for true ) for this problem

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
bool findTheFuckingAnswer(string A, string B, int &n, int &m, int i, int j, map<pair<int, int>, bool> &dp){
    
    if(i>=n and j>= m){
        return true;
    }
    if(j>=m) return false;
    
    if(dp.find({i,j})!=dp.end()) return dp[{i,j}];
    
    bool Ismatching  = (i<n and ((A[i] == B[j]) || (B[j] == '.')));
    if(j + 1 < m and B[j+1] == '*'){
        return dp[{i, j}] = findTheFuckingAnswer(A, B, n, m, i, j + 2,dp) || (Ismatching and findTheFuckingAnswer(A, B, n, m, i + 1, j, dp));
    }
    
    if(Ismatching){
        return dp[{i,j}] = findTheFuckingAnswer(A, B, n, m, i + 1, j + 1, dp);
    }
    return dp[{i,j}] = false;  
}

int Solution::isMatch(const string A, const string B) {
    
    int n = A.size();
    int m = B.size();
    map<pair<int, int>, bool> dp;
    
    return findTheFuckingAnswer(A, B, n, m, 0, 0, dp);
}
```