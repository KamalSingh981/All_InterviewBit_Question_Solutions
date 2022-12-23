# Burn a Tree | Interviewbit

Created: July 22, 2022 9:18 PM
Tags: Binary Trees, Graphs
URL: https://www.interviewbit.com/problems/burn-a-tree/

**Problem Description**

Given a binary tree denoted by root node **A** and a leaf node **B** from this tree.

It is known that all nodes connected to a given node **(left child, right child and parent)** get burned in 1 second. Then all the nodes which are connected through one intermediate get burned in 2 seconds, and so on.

You need to find the **minimum time** required to burn the complete binary tree.

**Problem Constraints**

2 <= number of nodes <= 105

1 <= node value, B <= 105

node value will be distinct

**Input Format**

First argument is a root node of the binary tree, A.

Second argument is an integer B denoting the node value of leaf node.

**Output Format**

Return an integer denoting the minimum time required to burn the complete binary tree.

**Example Input**

Input 1:

```
 Tree :      1
            / \
           2   3
          /   / \
         4   5   6
 B = 4
```

Input 2:

```
 Tree :      1
            / \
           2   3
          /     \
         4       5
 B = 5
```

**Example Output**

Output 1:

```
 4
```

Output 2:

```
 4
```

**Example Explanation**

Explanation 1:

```
 After 1 sec: Node 4 and 2 will be burnt.
 After 2 sec: Node 4, 2, 1 will be burnt.
 After 3 sec: Node 4, 2, 1, 3 will be burnt.
 After 4 sec: Node 4, 2, 1, 3, 5, 6(whole tree) will be burnt.

```

Explanation 2:

```
 After 1 sec: Node 5 and 3 will be burnt.
 After 2 sec: Node 5, 3, 1 will be burnt.
 After 3 sec: Node 5, 3, 1, 2 will be burnt.
 After 4 sec: Node 5, 3, 1, 2, 4(whole tree) will be burnt.

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
 
 
 // create mapping 
 // return target node
 TreeNode* createParentMapping(TreeNode* root,int target, map<TreeNode*, TreeNode*> & nodeToParent )
{
         TreeNode* res = NULL;
         queue<TreeNode*> q;
         q.push(root);
         nodeToParent[root] = NULL;
         
         while(!q.empty()){
             TreeNode* front = q.front();
             q.pop();
             
             if(front->val == target){
                 
                 res = front;
             }
             
             if(front->left){
                 nodeToParent[front->left] = front;
                 q.push(front->left);
             }
             
             if((front->right)){
                 nodeToParent[front->right] = front;
                 q.push(front->right);
             }
         }      
         return res; 
 }
 
 int burnTree(TreeNode* root, map<TreeNode*, TreeNode*> & nodeToParent){
     map<TreeNode*, bool> visited;
     queue<TreeNode*> q;
     
     q.push(root);
     visited[root] = true;;
     
     int ans = 0;
     
     while(!q.empty()){
         bool flag = 0;
         int size = q.size();
         for(int i = 0; i<size; i++){
             // process neighbouring nodes
             TreeNode* front = q.front();
             q.pop();
             if(front->left && !visited[front->left]){
                 flag = 1;
                 q.push(front->left);
                 visited[front->left] = 1;
             }
             if(front->right && !visited[front->right]){
                 q.push(front->right);
                 flag = 1;
                 visited[front->right] = 1;
             }
             
             if(nodeToParent[front] && !visited[nodeToParent[front]]){
                 flag = 1;
                 q.push(nodeToParent[front]);
                 visited[nodeToParent[front]] = 1; 
             }
         }     
         if(flag == 1){
             ans++;         }
     }
     return ans;   
 }
int Solution::solve(TreeNode* A, int B) {
    
    map<TreeNode*, TreeNode*> nodeToParent;
    TreeNode*tageNode = createParentMapping(A, B, nodeToParent);
    int ans = burnTree(tageNode, nodeToParent);
    
    return ans;
}
```