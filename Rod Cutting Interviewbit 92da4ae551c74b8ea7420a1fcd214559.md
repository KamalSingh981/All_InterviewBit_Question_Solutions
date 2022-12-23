# Rod Cutting | Interviewbit

Created: August 5, 2022 1:23 AM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/rod-cutting/

There is a rod of length N lying on x-axis with its left end at x = 0 and right end at x = N. Now, there are M weak points on this rod denoted by positive integer values(all less than N) A1, A2, …, AM. You have to cut rod at all these weak points. You can perform these cuts in any order. After a cut, rod gets divided into two smaller sub-rods. Cost of making a cut is the length of the sub-rod in which you are making a cut.

Your aim is to minimise this cost. Return an array denoting the sequence in which you will make cuts. If two different sequences of cuts give same cost, return the lexicographically smallest.

**Notes**:

- Sequence a, a ,…, a is lexicographically smaller than b, b ,…, b, if and only if at the first i where a and b differ, a < b, or if no such i found, then n < m.
    
    1
    
    2
    
    n
    
    1
    
    2
    
    m
    
    i
    
    i
    
    i
    
    i
    
- N can be upto 10.
    
    9
    

For example,

```
N = 6
A = [1, 2, 5]

If we make cuts in order [1, 2, 5], let us see what total cost would be.
For first cut, the length of rod is 6.
For second cut, the length of sub-rod in which we are making cut is 5(since we already have made a cut at 1).
For third cut, the length of sub-rod in which we are making cut is 4(since we already have made a cut at 2).
So, total cost is 6 + 5 + 4.

Cut order          | Sum of cost
(lexicographically | of each cut
 sorted)           |
___________________|_______________
[1, 2, 5]          | 6 + 5 + 4 = 15
[1, 5, 2]          | 6 + 5 + 4 = 15
[2, 1, 5]          | 6 + 2 + 4 = 12
[2, 5, 1]          | 6 + 4 + 2 = 12
[5, 1, 2]          | 6 + 5 + 4 = 15
[5, 2, 1]          | 6 + 5 + 2 = 13

So, we return [2, 1, 5].

```

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
void getAns(vector<int> &ans, vector<vector<int>> &dp, int i, int j, vector<int> p) {
    if (i + 1 == j) return ;
    for (int k = i + 1; k < j; k++) {
        if (dp[i][k] + dp[k][j] + p[j] - p[i] == dp[i][j]) {
            ans.push_back(p[k]);
            getAns(ans, dp, i, k, p);
            getAns(ans, dp, k, j, p);
            return ;
        }
    }
    return ;
}
vector<int> Solution::rodCut(int A, vector<int> &B) {
    vector<int> p;
    p.push_back(0);
    for (int b: B) p.push_back(b);
    p.push_back(A);
    sort(p.begin(), p.end());
    
    int n = p.size();
    vector<vector<int>> dp(n, vector<int>(n, 0));
    for (int l = 2; l <= n; l++) {
        for (int i = 0; i + l - 1 < n; i++) {
            dp[i][i+l-1] = INT_MAX;
            for (int k = i + 1; k < i + l - 1; k++)
                dp[i][i+l-1] = min(dp[i][i+l-1], dp[i][k] + dp[k][i+l-1] + p[i+l-1] - p[i]);
        }
                
    }
    
    vector<int> ans;
    getAns(ans, dp, 0, n - 1, p);
    return ans;
    
}
```