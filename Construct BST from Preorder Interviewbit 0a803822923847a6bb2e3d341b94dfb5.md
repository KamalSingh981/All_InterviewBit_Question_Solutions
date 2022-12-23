# Construct BST from Preorder | Interviewbit

Created: July 24, 2022 10:40 PM
Tags: Binary Trees, Recursion
URL: https://www.interviewbit.com/problems/construct-bst-from-preorder/

**Problem Description**

Given an integer array **A** with **distinct** elements, which represents the preorder traversal of a binary search tree,
 construct the tree and return its root.

A binary search tree is a binary tree where for every node, any descendant of Node.left has a value strictly less than Node.val, and any descendant of Node.right has a value strictly greater than Node.val.

A preorder traversal of a binary tree displays the value of the node first, then traverses Node.left, then traverses Node.right.

- *Problem Constraints**

1 <= |A| <= 105
 1 <= A.val <= 109
 The given array is a valid preorder traversal of a BST.

- *Input Format**
- *Output Format**
- *Example Input**

Input 1:

```
A = [2, 1, 4, 3, 5]

```

Input 2:

```
A = [1, 2, 3]

```

- *Example Output**

Output 1:

```
    2
   / \
  1   4
     / \
    3   5

```

Output 2:

```
      1
     /
    2
   /
  3

```

- *Example Explanation**

Explanation 1:

```
We can see that is the tree created by the given pre order traversal.
```

Explanation 2:

```
We can see that is the tree created by the given pre order traversal.

```

```cpp
TreeNode* build(vector <int>&A, int &i, int bound){
     if(i == A.size() || A[i] > bound) return NULL;
     TreeNode* root = new TreeNode (A[i++]);
     root->left = build(A, i, root->val);
     root->right = build(A, i, bound);
     return root;
 }
TreeNode* Solution::constructBST(vector<int> &A) {
    int i = 0;
    return build(A, i, INT_MAX);
}
```