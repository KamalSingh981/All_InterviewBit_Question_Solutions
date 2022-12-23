# Nodes at Distance K | Interviewbit

Created: July 24, 2022 1:54 AM
Tags: Binary Trees, Recursion
URL: https://www.interviewbit.com/problems/nodes-at-distance-k/

**Problem Description**

Given the root of a binary tree **A**, the value of a target node **B**, and an integer **C**, return an array of the values of all nodes that have a distance **C** from the target node.

You can return the answer in any order.

**Problem Constraints**

1 ≤ N ≤ 105 (N is the number of nodes in the binary tree)
1 ≤ Ai ≤ N (Ai denotes the values of the nodes in the tree)
All the values in the nodes are unique.
1 ≤ C ≤ 104

**Input Format**

The first argument is the root node of the binary tree A.
The second argument is an integer B denoting the label of the target node.
The third argument is an integer C denoting the distance.

**Output Format**

Return an array of integers denoting the nodes which are at a distance C from the node B.

**Example Input**

Input 1:

```
A =     1
       / \
      2   3
     / \
    4   5

B = 2
C = 1

```

Input 2:

```
A =     1
       / \
      2   3
     / \
    4   5

B = 2
C = 2

```

**Example Output**

Output 1:

```
[1, 4, 5]

```

Output 2:

```
[3]

```

**Example Explanation**

Explanation 1:

For the given tree, we have target node as 2.
 All the nodes with are at distance 1, meaning the adjacent nodes are [1, 4, 5].

Explanation 2:

The given tree is same, and [3] is the only node with distance 2.

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
 
 void printATKLevel(TreeNode*  root, int k, vector<int> &ans){
     if(root == NULL) {
         return;
     }
     if(k == 0){
         ans.push_back(root->val);
         return;
     }
     printATKLevel(root->left, k-1, ans);
     printATKLevel(root->right, k-1, ans);
     
 }
 
 int printatdistK(TreeNode* root, int B, int C, vector<int> &ans){
     if(root == NULL){
         return -1;
     }
     if(root->val == B){
         printATKLevel(root, C, ans);
         return 0;
     }
     
     
     int DL = printatdistK(root->left, B, C, ans);
     if(DL!= -1){
         
         if(DL + 1 == C){
             ans.push_back(root->val);
         }
         else{
             printATKLevel(root->right, C -2 -DL, ans);
         }
         return DL + 1;
     }
     int DR = printatdistK(root->right,B, C, ans);
     if(DR != -1){
         
         if(DR + 1 == C){
              ans.push_back(root->val);
      
         }
         else{
             printATKLevel(root->left, C-2-DR, ans);
         }
         return DR + 1;
     }
     
     return -1;
 }
 
vector<int> Solution::distanceK(TreeNode* A, int B, int C) {
    vector<int> ans;
    printatdistK(A, B, C, ans);
    return ans;
}
```