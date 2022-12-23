# Populate Next Right Pointers Tree | Interviewbit

Created: July 24, 2022 2:39 PM
Tags: BFS, Binary Trees
URL: https://www.interviewbit.com/problems/populate-next-right-pointers-tree/

Given a binary tree

```
    struct TreeLinkNode {
      TreeLinkNode *left;
      TreeLinkNode *right;
      TreeLinkNode *next;
    }

```

Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to `NULL`.

Initially, all next pointers are set to `NULL`.

> 
> 
> 
> **Note:**
> 
> - You may only use constant extra space.

**Example :**

Given the following binary tree,

```
         1
       /  \
      2    3
     / \  / \
    4  5  6  7

```

After calling your function, the tree should look like:

```
         1 -> NULL
       /  \
      2 -> 3 -> NULL
     / \  / \
    4->5->6->7 -> NULL

```

> 
> 
> 
> **Note 1:** that using recursion has memory overhead and does not qualify for constant space. **Note 2:** The tree need not be a perfect binary tree.
> 

```cpp
/**
 * Definition for binary tree with next pointer.
 * struct TreeLinkNode {
 *  int val;
 *  TreeLinkNode *left, *right, *next;
 *  TreeLinkNode(int x) : val(x), left(NULL), right(NULL), next(NULL) {}
 * };
 */
void Solution::connect(TreeLinkNode* A) {
    
    queue<TreeLinkNode*> q;
    q.push(A);
    q.push(NULL);
    TreeLinkNode* previous= NULL;
    while(!q.empty()){
        TreeLinkNode* temp = q.front();
        if(temp == NULL){
            previous = NULL;
            q.pop();
            if(!q.empty()){
                q.push(NULL);
            }
        }
        else{
            temp->next = previous;
            previous = temp;
            q.pop();
            if(temp->right){
                q.push(temp->right);
            }
            if(temp ->left){
                q.push(temp->left);
            }
        }
    }
}
```