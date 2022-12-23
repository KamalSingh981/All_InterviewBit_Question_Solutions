# Max Distance | Interviewbit

Created: May 15, 2022 10:00 AM
URL: https://www.interviewbit.com/problems/max-distance/

**Problem Description**

Given an array **A** of integers, find the maximum of **j - i** subjected to the constraint of **A[i] <= A[j]**.

**Input Format**

First and only argument is an integer array A.

**Output Format**

Return an integer denoting the maximum value of j - i;

**Example Input**

**Example Output**

**Example Explanation**

Explanation 1:

```
 Maximum value occurs for pair (3, 4).
```

```cpp
int Solution::maximumGap(const vector<int> &A) {
    
    int a  = 0;
    int b = 0;
    int maxi=0;
    int n = A.size();
    int rmax[n];
    rmax[n-1] = A[n-1];
    for(int i = n-2; i>=0; i--){
        rmax[i] = max(A[i], rmax[i+1]);
    }
    while(b<n && a<n){
        if(A[a]<=rmax[b]){
            maxi = max(maxi, b-a);
            b += 1;
        }
        else{
            a = a+1;
        }
    }
    return maxi;
}
```