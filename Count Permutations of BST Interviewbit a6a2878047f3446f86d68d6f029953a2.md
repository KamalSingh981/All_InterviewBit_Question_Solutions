# Count Permutations of BST | Interviewbit

Created: August 10, 2022 1:43 AM
Tags: Dynamic Programming, Very Hard Question
URL: https://www.interviewbit.com/problems/count-permutations-of-bst/

You are given two positive integers A and B. For all permutations of [1, 2, …, A], we create a BST. Count how many of these have height B.

Notes:

1. Values of a permutation are sequentially inserted into the BST by general rules i.e in increasing order of indices.
2. Height of BST is maximum number of edges between root and a leaf.
3. Return answer modulo 10 + 7.
    
    9
    
4. Expected time complexity is worst case O(N).
    
    4
    
5. 1 ≤ N ≤ 50

For example,

```
A = 3, B = 1

Two permutations [2, 1, 3] and [2, 3, 1] generate a BST of height 1.
In both cases the BST formed is

    2
   / \
  1   3

Another example,
A = 3, B = 2
Return 4.

```

Next question, can you do the problem in O(N3)?

```cpp
from math import factorial as f
def C(n, k):
    return f(n) // f(k) // f(n - k)

values = {}

def B(n, k):
    if n < 2:
        if k < n:
            return 0
        else:
            return 1

    if (n, k) in values:
        return values[(n, k)]

    s = 0
    for r in range(n):
        s += C(n - 1, r) * B(r, k - 1) * B(n - 1 - r, k - 1)

    values[(n, k)] = s
    return s

def solution(n, k):
    return B(n, k) - B(n, k - 1)

class Solution:
    # @param A : integer
    # @param B : integer
    # @return an integer
    def cntPermBST(self, A, B):
        return solution(A, B + 1) % (10**9 + 7)
```