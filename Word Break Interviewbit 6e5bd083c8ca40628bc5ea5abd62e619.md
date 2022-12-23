# Word Break | Interviewbit

Created: August 7, 2022 3:37 AM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/word-break/

Given a string **A** and a dictionary of words **B**, determine if **A** can be segmented into a space-separated sequence of one or more dictionary words.

**Input Format:**

```
The first argument is a string, A.
The second argument is an array of strings, B.

```

**Output Format:**

```
Return 0 / 1 ( 0 for false, 1 for true ) for this problem.

```

**Constraints:**

```
1 <= len(A) <= 6500
1 <= len(B) <= 10000
1 <= len(B[i]) <= 20

```

**Examples:**

```
Input 1:
    A = "myinterviewtrainer",
    B = ["trainer", "my", "interview"]

Output 1:
    1

Explanation 1:
    Return 1 ( corresponding to true ) because "myinterviewtrainer" can be segmented as "my interview trainer".

Input 2:
    A = "a"
    B = ["aaa"]

Output 2:
    0

Explanation 2:
    Return 0 ( corresponding to false ) because "a" cannot be segmented as "aaa".

```

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
int find(unordered_map<string, int> &m, string &A, unordered_map<string, int> &dp){
    if(m.find(A) != m.end()) return 1;
    if(dp.find(A) != dp.end()) return dp[A];
    
    bool ans = false;
    
    int n = A.length();
    if(n>20){
        n = 20;
    }
    for(int i = 1; i<=n; i++){
        string word = A.substr(0, i);
        string rem = A.substr(i);
        if(m.find(word) != m.end()){
            ans = ans || find(m, rem, dp);
            if(ans){
                return dp[A] = 1;
            }
        }
    }
    return dp[A] = ans;
}

int Solution::wordBreak(string A, vector<string> &B) {
    unordered_map<string, int> m;
    unordered_map<string, int> dp;
    for(auto i:B){
        m[i]++;
    }
    
    return find(m, A, dp);
}
```