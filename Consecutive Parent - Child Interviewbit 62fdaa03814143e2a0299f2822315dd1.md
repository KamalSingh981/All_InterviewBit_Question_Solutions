# Consecutive Parent - Child | Interviewbit

Created: July 24, 2022 4:24 PM
Tags: Binary Trees, Recursion
URL: https://www.interviewbit.com/problems/consecutive-parent-child/

**Problem Description**

You are given the root of a binary tree **A**. You have to find out the number of parent - child relationship whose values are consecutive numbers.

**Problem Constraints**

**Input Format**

**Output Format**

**Example Input**

Input 1:

```
A =  2
    / \
   1   3

```

Input 2:

```
A =  5
    / \
   1   3
      / \
     1   4

```

**Example Output**

Output 1:

```
2

```

Output 2:

```
1

```

**Example Explanation**

Explanation 1:

```
(2, 1) and (2, 3) are the consecutive parent - child relationships.
```

Explanation 2:

```
(3, 4) is the only consecutive parent - child relationship.

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
 
 void count(TreeNode* root, int &ans){
     if(root == NULL){
         return;
     }
     if(root->left and abs(root->left->val - root->val) == 1){
         ans++;
     }
     if(root->right and abs(root->right->val - root->val) == 1){
         ans++;
     }
     count(root->left, ans);
     count(root->right, ans);
 }
int Solution::consecutiveNodes(TreeNode* A) {
    int ans= 0;
    count(A, ans);
    return ans;
}
```

```cpp
int ans;
void rec(TreeNode *root) {
    if(!root) return;
    if(root->left) {
        if(abs(root->val - root->left->val)==1) ans++;
        rec(root->left);
    } 
    if(root->right) {
        if(abs(root->val - root->right->val)==1) ans++;
        rec(root->right);
    } 
}
int Solution::consecutiveNodes(TreeNode* A) {
    ans=0;
    rec(A);
    return ans;
}
```