# N digit numbers with digit sum S | Interviewbit

Created: August 9, 2022 2:26 AM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/n-digit-numbers-with-digit-sum-s-/

Find out the number of `N` digit numbers, whose digits on being added equals to a given number `S`. Note that a valid number starts from digits `1-9` except the number `0` itself. i.e. leading zeroes are not allowed.

Since the answer can be large, output answer modulo `1000000007`

`N = 2, S = 4` 
 Valid numbers are `{22, 31, 13, 40}` 
 Hence output `4`.

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
int m = 1e9 +7;

int telltheanswer(int A, int B, int flag, vector<vector<int>> &dp){
    if(A == 0 and B == 0) return 1;
    if(B<0 || A<=0) return 0;
    
    if(dp[A][B] != -1) return dp[A][B];
    
    int ans = 0;
    
    if(flag){
        for(int i = 1; i<=9; i++){
            ans = (ans%m + telltheanswer(A-1, B - i, false, dp))%m;
        }
    }
    else{
        for(int i = 0; i<=9; i++){
            ans = (ans%m + telltheanswer(A-1, B - i, false, dp)%m)%m;
        }
    }
    return dp[A][B] = ans%m;
}

int Solution::solve(int A, int B) {
    vector<vector<int>> dp(A + 1, vector<int>(B+1, -1));
    
    return telltheanswer(A, B, true, dp);
}
```