# Palindromic Substrings | Interviewbit

Created: June 20, 2022 3:17 AM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/palindromic-substrings/

**Problem Description**

Given a string **A** consisting of only lowercase English letters. 
Return the number of substrings of **A** which are **palindrome**.

**Problem Constraints**

**Input Format**

**Output Format**

**Example Input**

**Example Output**

**Example Explanation**

Explanation 1:

```
The plaindrome substrings are "a", "b", "a" and "aba".
```

Explanation 2:

```
The plaindrome substrings are "a", "b", "c" and "d".
```

## Brute  Force Solution of Complexity O(N^3)

```cpp
bool ispalindrome(string s){
    int n = s.size();
    for(int i=0; i<n/2; i++){
        if(s[i] != s[n-i-1]){
            return false;
        }
    }
    return true;
}
int Solution::solve(string A) {
    int n = A.size();
    int ans = n;
    
    for(int i = 0; i<n; i++){
        for(int j = i+1; j<n; j++){
            if(ispalindrome(A.substr(i, j-i+1))){
                ans++;
            }
        } 
    }
    return ans;
}
```

Implementation using Dynamic Programming with  complexity of O(n^2)

```cpp
int Solution::solve(string A) {
    int n = A.size();
    bool ans[n][n] = {false};
    int resu = 0;

    int diff = 0;
    for(int diff = 0; diff<n; diff++){
        int i = 0;
        int j = i + diff;
        for(i,j; j<n and i<n; i++, j++){
            if(diff == 0){
                ans[i][j] = true;
                resu++;
            }
            else if(diff == 1){
                if(A[i] == A[j]){
                    ans[i][j] = true;
                    resu++;
                }
            }
            else{
                if(A[i]==A[j] && ans[i+1][j-1]){
                    ans[i][j] = true;
                    resu++;
                }
            }
        }
    }
    return resu;
}
```