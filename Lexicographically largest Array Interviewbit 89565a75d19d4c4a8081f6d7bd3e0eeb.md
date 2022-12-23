# Lexicographically largest Array | Interviewbit

Created: August 7, 2022 3:57 AM
Tags: Two pointers
URL: https://www.interviewbit.com/problems/lexicographically-largest-array/

**Problem Description**

Given an integer array **A** consisting of distinct elements.
 You are aksed to create a **lexicograhically largest** array **S = X + reverse(Y)** ('+' denotes concatenation) such that it satisfies the following conditions:

- len(S) <= len(A)
- X is the **prefix array** of array A and Y is the **suffix array** of array A.

**Note:** Array X or Y can be empty.

**Problem Constraints**

**Input Format**

First and only argument is an integer array A.

**Output Format**

Return an integer array denoting the lexicographically largest array S.

**Example Input**

Input 1:

```
 A = [4, 1, 3, 2]
```

Input 2:

```
 A = [10, 20, 30, 40]
```

**Example Output**

Output 1:

```
 [4, 2, 3, 1]
```

Output 2:

```
 [40, 30, 20, 10]
```

**Example Explanation**

Explanation 1:

```
 X = [4], Y = [1, 3, 2]. Reverse(Y) = [2, 3, 1]
 S = X + Reverse(Y) = [4, 2, 3, 1]
```

Explanation 2:

```
 X = [], Y = [10, 20, 30, 40]. Reverse(Y) = [40, 30, 20, 10]
 S = [40, 30, 20, 10]
```

```cpp
vector<int> Solution::solve(vector<int> &A) {
    
    int i = 0;
    int j = A.size() - 1;
    while(i < j){
        if(A[i] < A[j]) break;
        i++;
    }
    reverse(A.begin() + i, A.end());
    return A;   
}
```