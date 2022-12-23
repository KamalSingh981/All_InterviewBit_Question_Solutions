# Root to Leaf Paths With Sum | Interviewbit

Created: July 22, 2022 10:50 PM
Tags: Binary Trees, Graphs, Recursion
URL: https://www.interviewbit.com/problems/root-to-leaf-paths-with-sum/

Given a binary tree and a sum, find all root-to-leaf paths where each path’s sum equals the given sum.

For example:
 Given the below binary tree and sum = 22,

```
              5
             / \
            4   8
           /   / \
          11  13  4
         /  \    / \
        7    2  5   1

```

return

```cpp
void findpath(TreeNode* root, int B, vector<vector<int>> &ans, vector<int> a){
     if(root->right == NULL and root->left == NULL) {
         if(B == root->val){
            a.push_back(root->val);
            ans.push_back(a);
            }
         return;
     }
     **a.push_back(root->val);
     if(root->left){
         findpath(root->left, B - root->val, ans, a);
     }
     if(root->right){
         findpath(root->right, B- root->val, ans, a);
     }
 }
 
vector<vector<int> > Solution::pathSum(TreeNode* A, int B) {
    vector<vector<int>> ans;
    findpath(A, B, ans, {});
    return ans;
}
```