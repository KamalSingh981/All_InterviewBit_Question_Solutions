# Reverse Level Order | Interviewbit

Created: July 24, 2022 12:58 PM
Tags: Binary Trees
URL: https://www.interviewbit.com/problems/reverse-level-order/

**Problem Description**

Given a binary tree, return the **reverse level order traversal** of its nodes values. (i.e, from left to right and from last level to starting level).

**Problem Constraints**

1 <= number of nodes <= 5 * 105

1 <= node value <= 105

**Input Format**

First and only argument is a pointer to the root node of the Binary Tree, A.

**Output Format**

Return an integer array denoting the reverse level order traversal from left to right.

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
 [15, 7, 9, 20, 3]
```

Output 2:

```
 [3, 6, 2, 1]
```

**Example Explanation**

Explanation 1:

```
 Nodes as level 3 : [15, 7]
 Nodes at level 2: [9, 20]
 Nodes at level 1: [3]
 Reverse level order traversal will be: [15, 7, 9, 20, 3]
```

Explanation 2:

```
 Nodes as level 3 : [3]
 Nodes at level 2: [6, 2]
 Nodes at level 1: [1]
 Reverse level order traversal will be: [3, 6, 2, 1]
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
vector<int> Solution::solve(TreeNode* root) {
    queue<TreeNode*> q;
    q.push(root);
    q.push(NULL);
    vector<vector<int>> ans;
    vector<int> a;
    while(!q.empty()){
        TreeNode* temp = q.front();
        if(temp == NULL){
            ans.push_back(a);
            a.clear();
            q.pop();
            if(!q.empty()){
                q.push(NULL);
            }
        }
        else{
            a.push_back(temp->val);
            q.pop();
            if(temp->left){
                q.push(temp->left);
            }
            if(temp->right){
                q.push(temp->right);
            }
        }
    }
    reverse(ans.begin(), ans.end());
    for(auto i: ans){
        for(auto j: i){
            a.push_back(j);
        }
    }
    return a;
}
```

using stack

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
vector<int> Solution::solve(TreeNode* root) {
    queue<TreeNode*> q;
    q.push(root);
    stack<int> ans;
    vector<int> a;
    while(!q.empty()){
        TreeNode* temp = q.front();
        ans.push(temp->val);
        q.pop();
        if(temp->right){
            q.push(temp->right);
        }
        if(temp->left){
            q.push(temp->left);
        }
    }
    while(!ans.empty()){
        int t = ans.top();
        a.push_back(t);
        ans.pop();
    }
    return a;
}
```