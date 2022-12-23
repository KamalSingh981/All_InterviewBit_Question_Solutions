# Level Order | Interviewbit

Created: July 26, 2022 3:56 AM
Tags: Binary Trees, Graphs
URL: https://www.interviewbit.com/problems/level-order/

**Problem Description**

Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

**Input Format**

First and only argument is root node of the binary tree, A.

**Output Format**

Return a 2D integer array denoting the zigzag level order traversal of the given binary tree.

**Example Input**

Input 1:

```
    3
   / \
  9  20
    /  \
   15   7

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
 [
   [3],
   [9, 20],
   [15, 7]
 ]
```

Output 2:

```
 [
   [1]
   [6, 2]
   [3]
 ]
```

**Example Explanation**

Explanation 1:

```
 Return the 2D array. Each row denotes the traversal of each level.
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
 bool check(TreeNode* root, int minv, int maxv){
     if(root == NULL){
         return true;
     }
     
     if(root->val > minv and root->val < maxv and check(root->left, minv, root->val) and check(root->right, root->val, maxv)){
         return true;
     }
     return false;
 }
 
int Solution::isValidBST(TreeNode* A) {
    return check(A, INT_MIN, INT_MAX);
    
}
```