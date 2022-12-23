# Sum Root to Leaf Numbers | Interviewbit

Created: July 22, 2022 9:55 PM
Tags: Binary Trees, Graphs, Recursion
URL: https://www.interviewbit.com/problems/sum-root-to-leaf-numbers/

Given a binary tree containing digits from 0-9 only, each root-to-leaf path could represent a number.

An example is the root-to-leaf path `1->2->3` which represents the number `123`.

Find the total sum of all root-to-leaf numbers % 1003.

**Example :**

```
    1
   / \
  2   3

```

The root-to-leaf path `1->2` represents the number `12`.
 The root-to-leaf path `1->3` represents the number `13`.

Return the sum = `(12 + 13) % 1003 = 25 % 1003 = 25`.

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
 int sums(TreeNode* root, int value){
     value = (value*10 + root->val)%1003;
     
     if(root->left == NULL and root->right == NULL){
         return value;
     }
     int l1 = 0, r1 = 0;
    if(root->left) l1 = sums(root->left, value);
    if(root->right) r1 = sums(root->right, value);
    return (r1 + l1);
 }
 
int Solution::sumNumbers(TreeNode* A) {
    return sums(A, 0)%1003;
}
```