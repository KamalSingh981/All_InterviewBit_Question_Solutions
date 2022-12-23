# Convert Sorted List to Binary Search Tree | Interviewbit

Created: July 24, 2022 10:30 PM
Tags: BinarySearchTree, Graphs
URL: https://www.interviewbit.com/problems/convert-sorted-list-to-binary-search-tree/

Given a singly linked list where elements are sorted in ascending order, convert it to a height balanced BST.

> 
> 
> 
> **A height balanced BST :** a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.
> 

**Example :**

```cpp
TreeNode *res(vector<int> &arr, int start, int end){
    if(start > end) return nullptr;
    if(start == end) return new TreeNode(arr[start]);
    int mid = start + (end-start)/2;
    TreeNode *node = new TreeNode(arr[mid]);
    node->left = res(arr, start, mid-1);
    node->right = res(arr, mid+1, end);
    return node;
}
 
TreeNode* Solution::sortedListToBST(ListNode* A) {
    vector<int>arr;
    while(A != nullptr){
        arr.push_back(A->val);
        A = A->next;
    }
    return res(arr, 0, arr.size()-1);
}
```