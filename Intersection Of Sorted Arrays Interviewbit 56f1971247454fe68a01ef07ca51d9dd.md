# Intersection Of Sorted Arrays | Interviewbit

Created: May 19, 2022 8:53 PM
Tags: Two pointers
URL: https://www.interviewbit.com/problems/intersection-of-sorted-arrays/

**Problem Description**

Find the intersection of two sorted arrays. OR in other words, Given 2 sorted arrays, find all the elements which occur in both the arrays.

**Example:**

```
Input:
    A: [1 2 3 3 4 5 6]
    B: [3 3 5]

Output: [3 3 5]Input:
    A: [1 2 3 3 4 5 6]
    B: [3 5]Output: [3 5]

```

**NOTE : For the purpose of this problem ( as also conveyed by the sample case ), assume that elements that appear more than once in both arrays should be included multiple times in the final output.**

```cpp
vector<int> Solution::intersect(const vector<int> &A, const vector<int> &B) {
    vector<int> ans;
    int a = 0;
    int i = 0;
    while ( i < A.size() && a < B.size()) {
            if (A[i] == B[a]) {
                ans.push_back(A[i]);
                i++;
                a++;
            } else if (A[i] < B[a]) {
                i++;}
              else if(A[i] > B[a]){
                  a++;
              }
            }

    return ans;   
}
```