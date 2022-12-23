# Min Depth of Binary Tree | Interviewbit

Created: July 22, 2022 10:31 PM
Tags: Binary Trees, BinarySearchTree, Recursion
URL: https://www.interviewbit.com/problems/min-depth-of-binary-tree/

Given a binary tree, find its minimum depth.

The minimum depth is the number of nodes along the shortest path from the root node down to the nearest leaf node.

> 
> 
> 
> **NOTE :** The path has to end on a leaf node.
> 

**Example :**

min depth = 2.

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
int Solution::minDepth(TreeNode* A) {
    if(A->left == NULL and  A->right == nullptr){
        return 1;
    }
    int l = INT_MAX, r = INT_MAX;
    if(A->left != NULL)
    l = minDepth(A->left);
    if(A->right != NULL)
    r = minDepth(A->right);
    return min(l, r) + 1;
    
}
```