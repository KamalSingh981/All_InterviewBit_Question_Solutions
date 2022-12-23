# Balanced Binary Tree | Interviewbit

Created: July 24, 2022 2:17 AM
Tags: Binary Trees, Recursion
URL: https://www.interviewbit.com/problems/balanced-binary-tree/

Given a binary tree, determine if it is height-balanced.

> 
> 
> 
> **Height-balanced binary tree** : is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.
> 

Return `0 / 1` ( 0 for false, 1 for true ) for this problem

**Example :**

```
Input :
          1
         / \
        2   3

Return : True or 1

Input 2 :
         3
        /
       2
      /
     1

Return : False or 0
         Because for the root node, left subtree has depth 2 and right subtree has depth 0.
         Difference = 2 > 1.

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
 
int heightt(TreeNode*A){
    int height;
    if(A == NULL)   {
        height = 0;
        return 0;
    }
    
    int l = heightt(A->left);
    int r = heightt(A->right);
    
    height = max(l, r)+1 ;
    if(abs(l-r)<=1 and l != -1 and r != -1){
        return height;
    }
    else{
        return -1;
    }
}
int Solution::isBalanced(TreeNode* A) {
    if(heightt(A) != -1){
        return 1;
    }
    else{
        return 0;
    }
}
```