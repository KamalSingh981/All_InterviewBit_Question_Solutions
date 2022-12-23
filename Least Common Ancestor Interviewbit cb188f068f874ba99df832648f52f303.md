# Least Common Ancestor | Interviewbit

Created: July 23, 2022 12:04 PM
Tags: Binary Trees, Recursion
URL: https://www.interviewbit.com/problems/least-common-ancestor/

Find the lowest common ancestor in an unordered binary tree given two values in the tree.

> 
> 
> 
> **Lowest common ancestor :** the lowest common ancestor (LCA) of two nodes `v` and `w` in a tree or directed acyclic graph (DAG) is the lowest (i.e. deepest) node that has both `v` and `w` as descendants.
> 

**Example :**

```

        _______3______
       /              \
    ___5__          ___1__
   /      \        /      \
   6      _2_     0        8
         /   \
         7    4

```

For the above tree, the LCA of nodes `5` and `1` is `3`.

> 
> 
> 
> **LCA** = Lowest common ancestor
> 

Please note that LCA for nodes `5` and `4` is `5`.

> 
> 
> - You are given 2 values. Find the lowest common ancestor of the two nodes represented by `val1` and `val2`
> - No guarantee that `val1` and `val2` exist in the tree. If one value doesn’t exist in the tree then return -1.
> - There are no duplicate values.
> - You can use extra memory, helper functions, and can modify the node struct but, you can’t add a parent pointer.

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
bool check(TreeNode* root, int val){
    if(!root){
        return false;
    }
    if(root->val == val){
        return true;
    }
    if((root->left and check(root->left, val)) || check(root->right,val)){
        return true;
    }
    return false;
}

TreeNode * find(TreeNode* root, int B, int C){
    if(!root || root->val == B || root->val == C){
        return root;
    }
    auto l = find(root->left, B, C);
    auto r = find(root->right, B, C);
    
    if(l and r){
        return root;
    }
    return l?l:r;
}
int Solution::lca(TreeNode* root, int B, int C) {
    if(!check(root, B) or  !check(root, C)){
        return -1;
    }
    auto ans = find(root, B, C);
    if(ans){
        return ans->val;
    }
    return -1;

}
```