# ZigZag Level Order Traversal BT | Interviewbit

Created: July 24, 2022 2:23 PM
Tags: Binary Trees, Recursion
URL: https://www.interviewbit.com/problems/zigzag-level-order-traversal-bt/

Given a binary tree, return the zigzag level order traversal of its nodes’ values. (ie, from left to right, then right to left for the next level and alternate between).

**Example :** 
 Given binary tree

```
    3
   / \
  9  20
    /  \
   15   7

```

return

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
vector<vector<int> > Solution::zigzagLevelOrder(TreeNode* A) {
    queue<TreeNode*> q;
    q.push(A);
    q.push(NULL);
    vector<int> p;
    vector<vector<int>> a;
    int  flag = 1;
    while(!q.empty()){
        TreeNode* temp = q.front();
        if(temp == NULL){
            if(flag%2 == 0){
                reverse(p.begin(), p.end());
            }
            a.push_back(p);
            p.clear();
            q.pop();
            if(!q.empty()){
                q.push(NULL);
            }
            flag++;    
        }
        else{
            p.push_back(temp->val);
            q.pop();
            if(temp->left){
                q.push(temp->left);
            }
            if(temp->right){
                q.push(temp->right);
            }
        }
    }
    return a;
}
```