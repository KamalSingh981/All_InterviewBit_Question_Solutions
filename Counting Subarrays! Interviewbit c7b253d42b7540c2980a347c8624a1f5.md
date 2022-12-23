# Counting Subarrays! | Interviewbit

Created: June 12, 2022 9:08 PM
Tags: Two pointers
URL: https://www.interviewbit.com/problems/counting-subarrays/

**Problem Description**

Given an array **A** of **N** non-negative numbers and you are also given non-negative number **B**.

You need to find the **number of subarrays in A having sum less than B**. We may assume that there is no overflow.

**Problem Constraints**

**Input Format**

First argument is an integer array **A**.

Second argument is an integer **B**.

**Output Format**

Return an integer denoting the **number of subarrays in A having sum less than B**.

**Example Input**

Input 1:

```
 A = [2, 5, 6]
 B = 10

```

Input 2:

```
 A = [1, 11, 2, 3, 15]
 B = 10

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 The subarrays with sum less than B are {2}, {5}, {6} and {2, 5},

```

Explanation 2:

```
 The subarrays with sum less than B are {1}, {2}, {3} and {2, 3}

```

```cpp
int Solution::solve(vector<int> &A, int B) {
    int ans = 0;
    int i = 0;
    int j = 0;
    int n = A.size();
    int cumsum= 0;
    while(i<n){
        cumsum += A[i];
        while(cumsum>=B){
            cumsum -= A[j];
            j++;
        }
        ans += (i-j+1);
        i++;
    }
    return ans;
}
```