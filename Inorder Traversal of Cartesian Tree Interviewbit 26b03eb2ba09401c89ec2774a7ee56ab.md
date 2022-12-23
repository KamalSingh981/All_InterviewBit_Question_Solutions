# Inorder Traversal of Cartesian Tree | Interviewbit

Created: July 23, 2022 1:44 AM
Tags: Graphs, Heap
URL: https://www.interviewbit.com/problems/inorder-traversal-of-cartesian-tree/

Given an inorder traversal of a cartesian tree, construct the tree.

> 
> 
> 
> **Cartesian tree** : is a heap ordered binary tree, where the root is greater than all the elements in the subtree.
> 

> 
> 
> 
> **Note:** You may assume that duplicates do not exist in the tree.
> 

**Example :**

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
 TreeNode*build(vector<int> &v, int s, int e){
     if(s>e){
         return NULL;
     }
     
     int ind = -1, maxi = INT_MIN;
     for(int i = s; i<= e; i++){
         if(maxi < v[i]){
             maxi = v[i];
             ind = i;
         }
     }
     
     TreeNode* root = new TreeNode(v[ind]);
     root->left = build(v, s, ind -1);
     root->right = build(v, ind +1 ,e);
     return root;
 }
TreeNode* Solution::buildTree(vector<int> &A) {
    return build(A, 0, A.size()-1);
    
}
```