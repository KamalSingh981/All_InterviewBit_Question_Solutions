# Kth Smallest Element In Tree | Interviewbit

Created: July 22, 2022 5:27 PM
Tags: BinarySearchTree, Graphs
URL: https://www.interviewbit.com/problems/kth-smallest-element-in-tree/

Given a binary search tree, write a function to find the kth smallest element in the tree.

**Example :**

```
Input :
  2
 / \
1   3

and k = 2

Return : 2

As 2 is the second smallest element in the tree.

```

> 
> 
> 
> **NOTE :** You may assume `1 <= k <= Total number of nodes in BST`
> 

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
 int ans = 0;
 int k =0;
 void kthelement(TreeNode* root, int B){
    if(root == NULL){
         return;
         
    }
    kthelement(root->left, B);
    k++;
    if(B == k){
        ans = root->val;
        return;
    }
    kthelement(root->right, B);
 }
int Solution::kthsmallest(TreeNode* A, int B) {
    k = 0;
    kthelement(A, B);
    return ans;
}
```

This idea is that the in order traversal is in sorted form.