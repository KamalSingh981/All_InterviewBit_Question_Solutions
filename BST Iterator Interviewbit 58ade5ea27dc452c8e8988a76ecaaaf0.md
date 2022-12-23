# BST Iterator | Interviewbit

Created: July 22, 2022 7:10 PM
Tags: BinarySearchTree, Graphs
URL: https://www.interviewbit.com/problems/bst-iterator/

Implement an iterator over a binary search tree (BST). Your iterator will be initialized with the root node of a BST.

The first call to `next()` will return the smallest number in BST. Calling `next()` again will return the next smallest number in the BST, and so on.

> 
> 
> 
> **Note:** `next()` and `hasNext()` should run in average `O(1)` time and uses `O(h)` memory, where `h` is the height of the tree. Try to optimize the additional space complexity apart from the amortized time complexity.
> 

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

stack<TreeNode*> s;
BSTIterator::BSTIterator(TreeNode *root) {
    while(root){
        s.push(root);
        root=root->left;
    } 
}

/** @return whether we have a next smallest number */
bool BSTIterator::hasNext() {
    return !s.empty();
}

/** @return the next smallest number */
int BSTIterator::next() {
    TreeNode* topnode = s.top();
    s.pop();
    BSTIterator(topnode->right);
    return topnode->val;
}

/**
 * Your BSTIterator will be called like this:
 * BSTIterator i = BSTIterator(root);
 * while (i.hasNext()) cout << i.next();
 */
```

Inefficient Way of doing this question using heaps

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

priority_queue<int, vector<int>, greater<int>> p;
void fill(TreeNode*node, priority_queue<int, vector<int>, greater<int>> &p){
    if(node==NULL) return;
    
    fill(node->left, p);
    p.push(node->val);
    fill(node->right, p);
}
BSTIterator::BSTIterator(TreeNode *root) {
    fill(root, p);
}

/** @return whether we have a next smallest number */
bool BSTIterator::hasNext() {
    return !p.empty();
}

/** @return the next smallest number */
int BSTIterator::next() {
    int topnode = p.top();
    p.pop();
    return topnode;
}

/**
 * Your BSTIterator will be called like this:
 * BSTIterator i = BSTIterator(root);
 * while (i.hasNext()) cout << i.next();
 */
```