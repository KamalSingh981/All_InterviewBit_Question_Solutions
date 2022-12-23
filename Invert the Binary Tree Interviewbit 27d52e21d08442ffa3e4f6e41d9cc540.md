# Invert the Binary Tree | Interviewbit

Created: July 23, 2022 3:37 AM
Tags: Binary Trees, Recursion
URL: https://www.interviewbit.com/problems/invert-the-binary-tree/

**Problem Description**

Given a binary tree **A**, invert the binary tree and return it.

Inverting refers to making left child as the right child and vice versa.

**Problem Constraints**

**Input Format**

First and only argument is the head of the tree A.

**Output Format**

Return the head of the inverted tree.

**Example Input**

Input 1:

```

     1
   /   \
  2     3

```

Input 2:

```

     1
   /   \
  2     3
 / \   / \
4   5 6   7

```

**Example Output**

Output 1:

```

     1
   /   \
  3     2

```

Output 2:

```

     1
   /   \
  3     2
 / \   / \
7   6 5   4

```

**Example Explanation**

Explanation 1:

```
Tree has been inverted.

```

Explanation 2:

```
Tree has been inverted.

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

TreeNode* Solution::invertTree(TreeNode* node) {
    if(node == NULL){
        return NULL;
    }
    
    // swap the children
    TreeNode* temp = node->left;
    node->left = node->right;
    node->right = temp;
    
    invertTree(node->left);
    invertTree(node->right);
    return node;
}
```