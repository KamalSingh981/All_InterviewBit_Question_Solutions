# Preorder Traversal | Interviewbit

Created: July 24, 2022 3:53 AM
Tags: Binary Trees, Recursion
URL: https://www.interviewbit.com/problems/preorder-traversal/

Given a binary tree, return the preorder traversal of its nodes’ values.

**Example :**
 Given binary tree

```
   1
    \
     2
    /
   3

```

return `[1,2,3]`.

**Using recursion is not allowed.**

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

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
void preorder(TreeNode * root, vector<int> &ans){
     if(root == NULL){
         return;
     }
     ans.push_back(root->val);
     preorder(root->left, ans);    
     preorder(root->right, ans);
}
vector<int> Solution::preorderTraversal(TreeNode* A) {
    vector<int> ans;
    preorder(A, ans);
    return ans;
}
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
void preorder(TreeNode * root, vector<int> &ans){
     if(root == NULL){
         return;
     }
     ans.push_back(root->val);
     preorder(root->left, ans);    
     preorder(root->right, ans);
}
vector<int> Solution::preorderTraversal(TreeNode* A) {
    vector<int> ans;
    preorder(A, ans);
    return ans;
}
```