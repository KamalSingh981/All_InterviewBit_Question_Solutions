# Palindrome Partitioning II | Interviewbit

Created: August 7, 2022 3:13 AM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/palindrome-partitioning-ii/

Given a string **A**, partition **A** such that every substring of the partition is a palindrome.

Return the **minimum** cuts needed for a palindrome partitioning of **A**.

**Input Format:**

```
The first and the only argument contains the string A.

```

**Output Format:**

```
Return an integer, representing the answer as described in the problem statement.

```

**Constraints:**

```
1 <= length(A) <= 501

```

**Examples:**

```
Input 1:
    A = "aba"

Output 1:
    0

Explanation 1:
    "aba" is already a palindrome, so no cuts are needed.

Input 2:
    A = "aab"

Output 2:
    1

Explanation 2:
    Return 1 since the palindrome partitioning ["aa","b"] could be produced using 1 cut.

```

```cpp
bool isPalindrome(string &A, int i, int j){
    while(i<j){
        if(A[i] != A[j]){
            return false;
        }
        i++;
        j--;
    }
    return true;
}

int f(int i, int n, string &A, vector<int> &dp){
    if(i == n) return 0;
    
    if(dp[i] != -1) return dp[i];
    
    
    int minCost = INT_MAX;
    for(int j = i; j<n; j++){
        if(isPalindrome(A, i, j)){
           minCost = min(minCost, 1 + f(j +1, n, A, dp));
           
        }
        
    }
    return dp[i] = minCost;
}

int Solution::minCut(string A) {
    
    vector<int> dp(A.length(), -1);
    return f(0,A.size(), A, dp)-1;
}
```