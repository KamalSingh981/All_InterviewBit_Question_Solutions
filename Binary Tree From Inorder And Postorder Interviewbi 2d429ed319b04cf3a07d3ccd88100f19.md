# Binary Tree From Inorder And Postorder | Interviewbit

Created: July 23, 2022 3:15 AM
Tags: Binary Trees, Recursion
URL: https://www.interviewbit.com/problems/binary-tree-from-inorder-and-postorder/

Given inorder and postorder traversal of a tree, construct the binary tree.

> 
> 
> 
> **Note:** You may assume that duplicates do not exist in the tree.
> 

**Example :**

```
Input :
        Inorder : [2, 1, 3]
        Postorder : [2, 3, 1]

Return :
            1
           / \
          2   3

```

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
int findIndex(vector<int> &inorder, int i, int j, int val)
{
    for (auto b = i; b<=j; ++b)
        if (inorder[b]==val)
            return b;
}
TreeNode* makeTree(vector<int> &inorder, vector<int> &postorder, int i, int j, int& p)
{
    if (i>j)
        return NULL;
    TreeNode* node = new TreeNode(postorder[p--]);
    if (i==j)
        return node;
    int in = findIndex(inorder, i, j, node->val);
    node->right = makeTree(inorder, postorder, in + 1, j, p);
    node->left = makeTree(inorder,postorder,i, in -1, p);
    return node;
}
TreeNode* Solution::buildTree(vector<int> &inorder, vector<int> &postorder) {
    if (postorder.empty() || inorder.empty())
        return NULL;
    int p = inorder.size() -1;
    return makeTree(inorder, postorder, 0, inorder.size()-1, p);
}
```