# Max Depth of Binary Tree | Interviewbit

Created: July 22, 2022 7:32 PM
Tags: Binary Trees, Graphs
URL: https://www.interviewbit.com/problems/max-depth-of-binary-tree/

Given a binary tree, find its maximum depth.

The maximum depth of a binary tree is the number of nodes along the longest path from the root node down to the farthest leaf node.

> 
> 
> 
> **NOTE :** The path has to end on a leaf node.
> 

**Example :**

max depth = 2.

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
int Solution::maxDepth(TreeNode* A) {
    if(A == NULL){
        return 0;
    }
    int lheight = maxDepth(A->left);
    int rheight = maxDepth(A->right);
    int height = max(lheight, rheight) +1;
    return height;
    
}
```