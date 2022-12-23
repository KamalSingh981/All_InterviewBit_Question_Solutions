# Regular Expression Match | Interviewbit

Created: August 9, 2022 11:49 PM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/regular-expression-match/

Implement wildcard pattern matching with support for ‘?’ and ‘*’ for strings **A** and **B**.

- ’?’ : Matches any single character.
- ‘*’ : Matches any sequence of characters (including the empty sequence).

The matching should cover the entire input string (not partial).

**Input Format:**

```
The first argument of input contains a string A.
The second argument of input contains a string B.

```

**Output Format:**

```
Return 0 or 1:
    => 0 : If the patterns do not match.
    => 1 : If the patterns match.

```

**Constraints:**

```
1 <= length(A), length(B) <= 9e4

```

**Examples :**

```
Input 1:
    A = "aa"
    B = "a"

Output 1:
    0

Input 2:
    A = "aa"
    B = "aa"

Output 2:
    1

Input 3:
    A = "aaa"
    B = "aa"

Output 3:
    0

Input 4:
    A = "aa"
    B = "*"

Output 4:
    1

Input 5:
    A = "aa"
    B = "a*"

Output 5:
    1

Input 6:
    A = "ab"
    B = "?*"

Output 6:
    1

Input 7:
    A = "aab"
    B = "c*a*b"

Output 7:
    0

```

```cpp
int Solution::isMatch(const string _A, const string _B) {

    // to make strings one indexed 
    // because we need to consider empty strings too
    // so it is better to make it one indexed
    string A = ' '+ _A;
    string B = ' '+ _B;
    int n = A.size();
    int m = B.size();

    vector<vector<bool>> dp(n,vector<bool>(m,false));
    // dp[i][j] represents matching first i characters of A
    // with first j characters of B

    for(int i =0;i<n;i++){
        for(int j = 0;j<m;j++){
            // matching empty string
            // if there are two empty strings then 
            // their match would be true
            if(i==0 && j==0){
                dp[i][j] = true;
                continue;
            }
            if(i==0){
                if(B[j]=='*')dp[i][j] = dp[i][j-1];
                // otherwise default value is false
                // if our A is ""(empty string)
                // are our B is "**" then dp[i][2] = dp[i][1] = dp[i][0] = true
                // and if B is "a*" then dp[i][2] = dp[i][1] = false
                continue;
            }
            if(j==0){
                //default value is false
                // i>0 and j = 0 
                // there is no way to match this string
                // A="a", B = ""
                continue;
            }
            if(B[j]=='?'|| A[i]==B[j]){
                // in this case we can match one characters
                // A = aac , B = aa? , then dp[3][3] = dp[2][2] = true
                // A = abc , B = ab? , then dp[3][3] = dp[2][2] = false

                // abc , abc ab = ab  => true
                // A = acb , B = abb, A = ac B = ab  => false
                // A = acb, B = ac? -> acb
                dp[i][j] = dp[i-1][j-1];
            }
            else if (B[j]=='*'){
                // we can match any number of characters including zero
                // zero characters
                // A = aa, B = aa* , then dp[2][3] = dp[2][2] that is dp[i][j-1] = true
                // more than zero characters
                // dp[i][j] = dp[i-1][j]
                // A = acbc, B = aa*, then - > B= aa*c -> B = aabc
                // dp[4][3] = dp[3][3] = true;
                // dp[3][3] = dp[2][3] = true 
                dp[i][j] = dp[i-1][j] || dp[i][j-1];
            }
        }
    }
    // returning  the final match value of whole A and B string 
    return dp[n-1][m-1];
}
```