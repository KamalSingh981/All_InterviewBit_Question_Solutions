# Valid Binary Search Tree | Interviewbit

Created: July 26, 2022 1:42 AM
Tags: BinarySearchTree
URL: https://www.interviewbit.com/problems/valid-binary-search-tree/

Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

1. The left subtree of a node contains only nodes with keys less than the node’s key.
2. The right subtree of a node contains only nodes with keys greater than the node’s key.
3. Both the left and right subtrees must also be binary search trees.

**Example :**

```
Input :
   1
  /  \
 2    3

Output : 0 (False)

Input :
  2
 / \
1   3

Output : 1 (True)

```

Return `0 / 1` ( 0 for false, 1 for true ) for this problem

**SOLUTION APPROACH :**
 VIDEO : https://www.youtube.com/watch?v=yEwSGhSsT0U

Complete solution in the hints.

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
 bool check(TreeNode* root, int minv, int maxv){
     if(root == NULL){
         return true;
     }
     
     if(root->val > minv and root->val < maxv and check(root->left, minv, root->val) and check(root->right, root->val, maxv)){
         return true;
     }
     return false;
 }
 
int Solution::isValidBST(TreeNode* A) {
    return check(A, INT_MIN, INT_MAX);
    
}
```