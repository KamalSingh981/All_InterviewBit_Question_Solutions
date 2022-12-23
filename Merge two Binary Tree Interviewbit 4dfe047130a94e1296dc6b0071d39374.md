# Merge two Binary Tree | Interviewbit

Created: July 24, 2022 3:18 AM
Tags: Binary Trees, Recursion
URL: https://www.interviewbit.com/problems/merge-two-binary-tree/

**Problem Description**

Given two Binary Trees **A** and **B**, you need to **merge** them in a single binary tree.

The merge rule is that if two nodes overlap, then sum of node values is the new value of the merged node.

Otherwise, the non-null node will be used as the node of new tree.

**Problem Constraints**

1 <= Number of Nodes in A , B <= 105

**Input Format**

First argument is an pointer to the root of binary tree **A**.

Second argument is an pointer to the root of binary tree **B**.

**Output Format**

Return a pointer to the root of new binary tree.

**Example Input**

Input 1:

```
 A =   2

      / \

     1   4

    /

   5

B =   3
      / \
      6  1
      \   \
       2   7

```

Input 2:

```
 A =   12

      / \

     11  14

B =   3
      / \
      6  1

```

**Example Output**

Output 1:

```
     5
    / \
   7   5
  / \   \
 5   2   7

```

Output 2:

```
   15
  / \
 17  15

```

**Example Explanation**

Explanation 1:

```
 After merging both the trees you get:
     5
    / \
   7   5
  / \   \
 5   2   7

```

Explanation 2:

```
 After merging both the trees we get:
   15
  / \
 17  15

```

```cpp
/**
 * Definition for binary tree
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
TreeNode* Solution::solve(TreeNode* A, TreeNode* B) {
    if(A == NULL) return B;
    if(B == NULL) return A;
    A->val += B->val;
    A -> left = solve(A->left, B->left);
    A -> right = solve(A->right, B->right);
    return A;
}
```