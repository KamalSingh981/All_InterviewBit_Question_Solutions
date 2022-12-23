# Smaller or equal elements | Interviewbit

Created: May 24, 2022 3:02 AM
Tags: Binary Search, Easy
URL: https://www.interviewbit.com/problems/smaller-or-equal-elements/

**Problem Description**

Given an sorted array **A** of size **N**. Find number of elements which are less than or equal to **B**.

**NOTE:** Expected Time Complexity O(log N)

**Problem Constraints**

**Input Format**

First agument is an integer array A of size N.

Second argument is an integer B.

**Output Format**

Return an integer denoting the number of elements which are less than or equal to **B**.

**Example Input**

Input 1:

```
 A = [1, 3, 4, 4, 6]
 B = 4
```

Input 2:

```
 A = [1, 2, 5, 5]
 B = 3
```

**Example Output**

**Example Explanation**

Explanation 1:

```
 Elements (1, 3, 4, 4) are less than or equal to 4.
```

Explanation 2:

```
 Elements (1, 2) are less than or equal to 3.
```

```cpp
int index(vector<int> A, int B){
    int l = 0;
    int r = A.size()-1;
    int mid;
    while(l<=r){
        mid = l + (r-l)/2;
        if(A[mid] <= B){
            l = mid+1;
        }
        if(A[mid]>B){
            r = mid-1;
        }
    }
    return l;
}

int Solution::solve(vector<int> &A, int B) {
    return index(A, B);
}
```