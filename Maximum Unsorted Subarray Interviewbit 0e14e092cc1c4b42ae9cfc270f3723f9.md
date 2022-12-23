# Maximum Unsorted Subarray | Interviewbit

Created: May 15, 2022 11:02 AM
URL: https://www.interviewbit.com/problems/maximum-unsorted-subarray/

**Problem Description**

Given an array **A** of non-negative integers of size **N**. Find the minimum sub-array **Al, Al+1 ,..., Ar** such that if we sort(in ascending order) that sub-array, then the whole array should get sorted. If **A** is already sorted, output **-1**.

**Problem Constraints**

**Input Format**

First and only argument is an array of non-negative integers of size N.

**Output Format**

Return an array of length two where the first element denotes the starting index(0-based) and the second element denotes the ending index(0-based) of the sub-array. If the array is already sorted, return an array containing only one element i.e. -1.

**Example Input**

Input 1:

```
A = [1, 3, 2, 4, 5]
```

Input 2:

```
A = [1, 2, 3, 4, 5]
```

**Example Output**

**Example Explanation**

Explanation 1:

```
If we sort the sub-array A1, A2, then the whole array A gets sorted.
```

Explanation 2:

```
A is already sorted.
```

```cpp
vector<int> Solution::subUnsort(vector<int> &A) {
    int n = A.size();
    int a = 0;
    int b = n-1;
    int maxi;
    int mini;
    for(a=0; a<n-1; a++){
        if(A[a] > A[a+1]){
            break;
        }
    }
    vector<int> ans;
    ans.push_back(-1);
    if(a == n-1){
        return ans;
    }

    for(b=n-1; b>0; b--) {
        if (A[b] < A[b - 1]) {
            break;
        }
    }
    maxi = A[a]; mini = A[a]; 
    for(int i = a+1; i <= b; i++) {
        if(A[i]>maxi){
            maxi = A[i];
        }
        if(A[i]<mini){
            mini = A[i];
        }
    }

    for(int i = 0; i<a; i++){
        if(A[i]>mini){
            a = i;
            break;
        }
    }
    for(int i = n-1; i>=b+1; i--){
        if(A[i]<maxi){
            b = i;
            break;
        }
    }
    ans.clear();
    ans.push_back(a);
    ans.push_back(b);
    return ans;
}
```