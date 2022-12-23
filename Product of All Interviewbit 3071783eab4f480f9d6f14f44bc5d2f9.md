# Product of All | Interviewbit

Created: May 9, 2022 1:51 AM
URL: https://www.interviewbit.com/problems/product-of-all/

**Problem Description**

Given an integer array **A**.
Create an array **B** such that **Bi** is the **product of all elements of A excluding Ai**.
Since the products can be too large take **modulo 109 +7**.

**Problem Constraints**

**Input Format**

**Output Format**

**Example Input**

**Example Output**

**Example Explanation**

Explanation 1:

```
[2×3×4, 1×3×4, 1×2×4, 1×2×3]
```

Explanation 2:

```
[9×9×9, 9×9×9, 9×9×9]
```

```cpp
vector<int> Solution::solve(vector<int> &A) {
    int mod = (1e9+7);
    int n = A.size();
    long long pre[n], suf[n];
    pre[0] = 1;
    for(int i=1; i<n; ++i){
        pre[i] = (pre[i-1]*A[i-1])%mod;
    }
    suf[n-1] = 1;
    for(int i=n-2; i>=0; --i){
        suf[i] = (suf[i+1]*A[i+1])%mod;
    }
    vector<int> ans(n);
    for(int i=0; i<n; ++i){
        ans[i] = (pre[i]*suf[i])%mod;
    }
    return ans;
}
```