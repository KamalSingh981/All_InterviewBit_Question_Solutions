# Recover Binary Search Tree | Interviewbit

Created: July 12, 2022 2:01 AM
Tags: BinarySearchTree
URL: https://www.interviewbit.com/problems/recover-binary-search-tree/

Two elements of a binary search tree (BST) are swapped by mistake.
 Tell us the 2 values swapping which the tree will be restored.

> 
> 
> 
> **Note:** A solution using O(n) space is pretty straight forward. Could you devise a constant space solution?
> 

**Example :**

```

Input :
         1
        / \
       2   3

Output :
       [1, 2]

Explanation : Swapping 1 and 2 will change the BST to be
         2
        / \
       1   3
which is a valid BST

```

Code From the YouTube

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
 
 void Inorder(TreeNode* a, TreeNode** first, TreeNode** mid, TreeNode** last, TreeNode** prev){
     if(a == NULL){
         return;
     }
     
     
     //Recursive case
     Inorder(a->left, first, mid, last, prev);
     
     if(*prev && a->val < (*prev)->val){
         if(!*first){
             *first = *prev;
             *mid = a;
         }
         else{
             *last = a;
         }
     }
     *prev = a;
     Inorder(a->right, first, mid, last, prev);
 }
 
 
vector<int> Solution::recoverTree(TreeNode* A) {
    vector<int> ans;
    TreeNode* first, *mid, *last, *prev;
    first = NULL;
    mid = NULL;
    last = NULL;
    prev = NULL;
    
    Inorder(A, &first, &mid, &last, &prev);
    
    
    if(first && last){
        ans.push_back(last->val);
        ans.push_back(first->val);
        
    }
    
    else if(first and mid){
        ans.push_back(mid->val);
        ans.push_back(first->val);
    }
    return ans;
}
```

My Code

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
 
 void Inorder(TreeNode* a, vector<int> &inor){
     if(a == NULL){
         return;
     }
     
     
     //Recursive case
     Inorder(a->left, inor);
     inor.push_back(a->val);
     Inorder(a->right, inor);
 }
 
 
vector<int> Solution::recoverTree(TreeNode* A) {
    vector<int> a;
    Inorder(A, a);
    int c = 0;
    int val1;
    int val2;
    bool ones = true;
    for(int i = 1; i<a.size(); i++){
        if(a[i]<a[c] and ones){
            val1 = a[c];
            val2 = a[i];
            ones = false;
        }
        else if(a[i]<a[c] && ones == false){
            val2 = a[i];
            break;
        } 
        c++;
    }
    a.clear();
    a.push_back(val2);
    a.push_back(val1);
    return a;
}
```