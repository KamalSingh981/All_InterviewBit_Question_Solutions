# Length of Longest Subsequence | Interviewbit

Created: July 31, 2022 4:55 PM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/length-of-longest-subsequence/

**Problem Description**

Given an 1D integer array **A** of length **N**, find the length of longest subsequence which is first increasing then decreasing.

**Problem Constraints**

**Input Format**

The first and the only argument contains an integer array **A**.

**Output Format**

Return an integer representing the answer as described in the problem statement.

**Example Input**

Input 1:

```
 A = [1, 2, 1]

```

Input 2:

```
 A = [1, 11, 2, 10, 4, 5, 2, 1]

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 [1, 2, 1] is the longest subsequence.

```

Explanation 2:

```
 [1 2 10 4 2 1] is the longest subsequence.

```

```cpp
int Solution::longestSubsequenceLength(const vector<int> &A) {
    
    int n = A.size();
    int lis[n];
    int lds[n];
    for(int i = 0; i<n; i++){
        lis[i] = 1;
        lds[i] = 1;
    }
    
    for(int i = 1; i<n; i++){
        for(int j = 0; j<i; j++){
            if(A[i]>A[j] and lis[i]< lis[j] + 1){
                lis[i] = lis[j] +1;
            }
        }
    }
    for(int i = n-2; i>=0; i--){
        for(int j = n-1; j>=i; j--){
            if(A[i]>A[j] and lds[i]< lds[j] + 1){
                lds[i] = lds[j] +1;
            }
        }
    }
    int ans = 0;
    for(int i =0; i<n; i++){
        ans = max(ans, lis[i] + lds[i] - 1);
    }
    return ans;
}
```