# Highest Product | Interviewbit

Created: July 25, 2022 12:36 PM
Tags: GreedyAlgorithm
URL: https://www.interviewbit.com/problems/highest-product/

Given an array **A**, of **N** integers A.

Return the highest product possible by multiplying 3 numbers from the array.

**NOTE:** Solution will fit in a 32-bit signed integer.

**Input Format:**

The first and the only argument is an integer array A.

**Output Format:**

Return the highest possible product.

**Constraints:**

1 <= N <= 5e5

**Example:**

```cpp
int Solution::maxp3(vector<int> &A) {
    sort(A.begin(), A.end());
    int n = A.size();
    int ans = 1;
    // There can only be two possible candidates for possible answers
    ans = max(A[n-1]* A[n-2]*A[n-3], A[0]*A[1]*A[n-1]); 
    return ans;
}
```