# Sorted Array To Balanced BST | Interviewbit

Created: July 23, 2022 2:00 AM
Tags: Binary Trees, Recursion
URL: https://www.interviewbit.com/problems/sorted-array-to-balanced-bst/

Given an array where elements are sorted in ascending order, convert it to a height balanced BST.

> 
> 
> 
> **Balanced tree :** a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.
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
 
 TreeNode * balancedBT(const vector<int> &a, int s, int e){
     if(s> e){
         return NULL;
     }
     
     int mid = (s+e)/2;
     TreeNode*root = new TreeNode(a[mid]);
     root->left = balancedBT(a, s, mid -1);
     root->right = balancedBT(a, mid + 1, e);
     return root;
 }
TreeNode* Solution::sortedArrayToBST(const vector<int> &A) {
    return balancedBT(A, 0, A.size()- 1);
}
```