# Symmetric Binary Tree | Interviewbit

Created: July 24, 2022 3:35 AM
Tags: Binary Trees, Recursion
URL: https://www.interviewbit.com/problems/symmetric-binary-tree/

**Problem Description**

Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

**Problem Constraints**

**Input Format**

First and only argument is the root node of the binary tree.

**Output Format**

**Example Input**

Input 1:

```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

Input 2:

```
    1
   / \
  2   2
   \   \
   3    3
```

**Example Output**

**Example Explanation**

Explanation 1:

```
 The above binary tree is symmetric.
```

Explanation 2:

```
The above binary tree is not symmetric.
```

![Symmetric%20Binary%20Tree%20Interviewbit%20d4f01041f8c744f081bc775c9ef77ec0/superman.e804d3.png](Symmetric%20Binary%20Tree%20Interviewbit%20d4f01041f8c744f081bc775c9ef77ec0/superman.e804d3.png)

```cpp
bool find(TreeNode * A, TreeNode* B){
     if(A == NULL or B == NULL ) return (A == B);
     if(A->val  != B->val) return false;
     
     return find(A->left, B->right) and find(A->right, B->left);
 }
int Solution::isSymmetric(TreeNode* A) {
    bool ans = find(A->left, A->right);
    return ans;
}
```