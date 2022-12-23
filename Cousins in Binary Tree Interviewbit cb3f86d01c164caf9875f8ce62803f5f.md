# Cousins in Binary Tree | Interviewbit

Created: July 24, 2022 1:32 PM
Tags: Binary Trees, Recursion
URL: https://www.interviewbit.com/problems/cousins-in-binary-tree/

**Problem Description**

Given a Binary Tree **A** consisting of **N** nodes.

You need to find all the cousins of node **B**.

**NOTE:**

- Siblings should not be considered as cousins.
- Try to do it in single traversal.
- You can assume that Node **B** is there in the tree **A**.
- Order doesn't matter in the output.

**Problem Constraints**

**Input Format**

First Argument represents the root of binary tree **A**.

Second Argument is an integer **B** denoting the node number.

**Output Format**

Return an integer array denoting the cousins of node **B**.

**NOTE:** Order doesn't matter.

**Example Input**

Input 1:

```
 A =

           1
         /   \
        2     3
       / \   / \
      4   5 6   7

B = 5

```

Input 2:

```
 A =
            1
          /   \
         2     3
        / \ .   \
       4   5 .   6

B = 1

```

**Example Output**

Output 1:

```
 [6, 7]

```

Output 2:

**Example Explanation**

Explanation 1:

```
 Cousins of Node 5 are Node 6 and 7 so we will return [6, 7]
 Remember Node 4 is sibling of Node 5 and do not need to return this.

```

Explanation 2:

```
 Since Node 1 is the root so it doesn't have any cousin so we will return an empty array.

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
 void find(TreeNode* root, int B, int &k, int l){
     if(root == NULL){
         return;
     }
     if(root->val == B){
         k = l;
         return;
     }
     find(root->left, B, k, l+1);
     find(root->right, B, k,l+1);
 }
 
 void print(TreeNode* root, int B, int k, vector<int> &ans){
     if(root == NULL){
         return;
     }
     if(k == 1){
         if(root->left != NULL and root->left->val == B || root->right!=NULL and root->right->val == B){
             return;
         }
     }
     
     if(k == 0){
         ans.push_back(root->val);
     }
     print(root->left, B, k-1, ans);
     print(root->right, B, k-1, ans);
 }
 
vector<int> Solution::solve(TreeNode* A, int B) {
    vector<int> ans;
    int k = 0;
    find(A, B, k, 0);
    print(A, B, k, ans);
    return ans;
}
```