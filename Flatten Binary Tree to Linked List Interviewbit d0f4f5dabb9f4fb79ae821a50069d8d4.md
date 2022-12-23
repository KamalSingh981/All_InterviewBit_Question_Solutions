# Flatten Binary Tree to Linked List | Interviewbit

Created: July 24, 2022 3:14 PM
Tags: Binary Trees, Recursion
URL: https://www.interviewbit.com/problems/flatten-binary-tree-to-linked-list/

Given a binary tree, flatten it to a linked list in-place.

**Example :**
 Given

```

         1
        / \
       2   5
      / \   \
     3   4   6

```

The flattened tree should look like:

Note that the left child of all nodes should be `NULL`.

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
 
 TreeNode * helper(TreeNode* root){
     if(root == NULL){
         return NULL;
     }
     if(root->left == NULL and root->right == NULL){
         return root;
     }
     
     TreeNode* ltail = helper(root->left);
     TreeNode * rtail = helper(root->right);
     
     if(ltail and rtail){
         ltail->right = root->right;
         root->right = root->left;
         root->left = NULL;
     }
     else if(ltail){
         root->right = root->left;
         root->left = NULL;
         return ltail;
     }
     
     return rtail;
     
 }
TreeNode* Solution::flatten(TreeNode* A) {
    // Do not write main() function.
    // Do not read input, instead use the arguments to the function.
    // Do not print the output, instead return values as specified
    // Still have a doubt. Checkout www.interviewbit.com/pages/sample_codes/ for more details
    helper(A);
    return A;
}
```