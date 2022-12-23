# Identical Binary Trees | Interviewbit

Created: July 24, 2022 3:43 AM
Tags: Binary Trees, Recursion
URL: https://www.interviewbit.com/problems/identical-binary-trees/

Given two binary trees, write a function to check if they are equal or not.

Two binary trees are considered equal if they are structurally identical and the nodes have the same value.

Return **`0 / 1`** ( 0 for false, 1 for true ) for this problem

**Example :**

```
Input :

   1       1
  / \     / \
 2   3   2   3

Output :
  1

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
int Solution::isSameTree(TreeNode* A, TreeNode* B) {
    if(A == NULL || B==NULL){
        return (A==B);
    }
    
    if(A->val != B->val) return false;
    return (isSameTree(A->left, B->left) && isSameTree(A->right,B->right));
}
```