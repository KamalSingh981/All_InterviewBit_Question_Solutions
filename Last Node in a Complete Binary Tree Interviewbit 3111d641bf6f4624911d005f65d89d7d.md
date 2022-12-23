# Last Node in a Complete Binary Tree | Interviewbit

Created: July 24, 2022 4:43 PM
Tags: Binary Trees, Recursion
URL: https://www.interviewbit.com/problems/last-node-in-a-complete-binary-tree/

**Problem Descriptio**

You are given the root of a complete binary tree **A**.
 You have to return the value of the rightmost node in the last level of the binary tree.

Try to find a solution with a better time complexity than O(N).

**Problem Constraints**

**Input Format**

**Output Format**

Return a single integer denoting the value of the rightmost node in the last level of the binary tree.

**Example Input**

Input 1:

```
A =
    1
   /
  2

```

Input 2:

```
A =
    1
   / \
  2   3

```

**Example Output**

**Example Explanation**

Explanation 1:

```
There is only a single node in the last level of the binary tree.
Therefore, the answer is 2.
```

Explanation 2:

```
There a two nodes in the last level of the tree.
The rightmost nodes is 3.

```

Recursive solution

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
void findtheNode(TreeNode* root, int &ans, int level, int &maxlevel){
    if(root== NULL){
        return;
    }
    if(maxlevel<level){
        ans = root->val;
        maxlevel = level;
    }
    
    findtheNode(root->right, ans, level + 1, maxlevel);
    findtheNode(root->left, ans, level + 1 , maxlevel);
} 

int Solution::lastNode(TreeNode* A) {
    int ans = 0;
    int maxlevel  = -1;
    findtheNode(A, ans, 0, maxlevel);
    return ans; 
}
```

Iterative Solution

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
int Solution::lastNode(TreeNode* root) {
    queue<TreeNode*> q;
    q.push(root);
    int ans;
    while(!q.empty())
    {
        TreeNode* temp = q.front();
        ans = temp->val;
        q.pop();
        if(temp->left)
        {
            q.push(temp->left);
        }
        if(temp->right)
        {
            q.push(temp->right);
        }
    }
    return ans;
}
```