# Leaf Village | binarysearch

Created: August 11, 2022 3:13 PM
Tags: Binary Trees
URL: https://binarysearch.com/room/Leaf-Village-mCQs6YdVDF

Given a binary tree `root`, invert it so that its left subtree and right subtree are swapped and the children are recursively inverted.

**Constraints**

- `n ≤ 100,000` where `n` is the number of nodes in `root`

```cpp
Tree* solve(Tree* root) {
    if(root==NULL){
        return NULL;
    }

    Tree* r = solve(root->right);
    Tree* l = solve(root->left);
    root->left = r;
    root->right = l;

    return root; 
}
```