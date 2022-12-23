# Postorder Traversal | Interviewbit

Created: July 24, 2022 3:57 AM
Tags: Binary Trees, Recursion
URL: https://www.interviewbit.com/problems/postorder-traversal/

**Problem Description**

Given a binary tree, return the Postorder traversal of its nodes values.

**NOTE:** Using recursion is not allowed.

**Problem Constraints**

**Input Format**

First and only argument is root node of the binary tree, A.

**Output Format**

Return an integer array denoting the Postorder traversal of the given binary tree.

**Example Input**

Input 1:

```
   1
    \
     2
    /
   3
```

Input 2:

```
   1
  / \
 6   2
    /
   3
```

**Example Output**

Output 1:

```
 [3, 2, 1]
```

Output 2:

```
 [6, 3, 2, 1]
```

**Example Explanation**

Explanation 1:

```
 The Preoder Traversal of the given tree is [3, 2, 1].
```

Explanation 2:

```
 The Preoder Traversal of the given tree is [6, 3, 2, 1].
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
void postorder(TreeNode * root, vector<int> &ans){
     if(root == NULL){
         return;
     }
     
     postorder(root->left, ans);    
     postorder(root->right, ans);
     ans.push_back(root->val);
}
vector<int> Solution::postorderTraversal(TreeNode* A) {
    vector<int> ans;
    postorder(A, ans);
    return ans;
}
```