# Maximum Sum Triplet | Interviewbit

Created: May 9, 2022 1:46 AM
URL: https://www.interviewbit.com/problems/maximum-sum-triplet/

**Problem Description**

Given an array **A** containing **N** integers.

You need to find the **maximum sum of triplet** ( Ai + Aj + Ak ) such that 0 <= i < j < k < N and Ai < Aj < Ak.

If no such triplet exist return **0**.

**Problem Constraints**

3 <= N <= 105.

1 <= A[i] <= 108.

**Input Format**

First argument is an integer array **A**.

**Output Format**

Return a single integer denoting the maximum sum of triplet as described in the question.

**Example Input**

Input 1:

```
 A = [2, 5, 3, 1, 4, 9]

```

Input 2:

```
 A = [1, 2, 3]

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 All possible triplets are:-
    2 3 4 => sum = 9
    2 5 9 => sum = 16
    2 3 9 => sum = 14
    3 4 9 => sum = 16
    1 4 9 => sum = 14
  Maximum sum = 16

```

Explanation 2:

```
 All possible triplets are:-
    1 2 3 => sum = 6
 Maximum sum = 6

```

```cpp
#include <iostream>
#include <algorithm>
#include <bits/stdc++.h>
using namespace std;
int Solution::solve(vector<int> &A) {
    int l = A.size();
    vector<int>a(l);
    // suffix array:
    for(int i=l-1; i>=0; i--){
        if(i==l-1)a[i] = A[i];
        else{
            a[i] = max(a[i+1],A[i]);
        }
    }
    int ans = 0;
    set<int> s;
    s.insert(A[0]);
    for(int j = 1; j<l; j++){
        s.insert(A[j]);
        auto it = s.find(A[j]);
        if(it != s.begin() && a[j]!=A[j]){
            ans  = max(ans, (*--it) + A[j] + a[j]);
        }

    }
    return ans;
}
```