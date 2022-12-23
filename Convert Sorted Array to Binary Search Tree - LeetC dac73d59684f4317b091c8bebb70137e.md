# Convert Sorted Array to Binary Search Tree - LeetCode

Created: August 10, 2022 5:10 PM
Tags: BinarySearchTree, Daily Challenge
URL: https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/

Given an integer array `nums` where the elements are sorted in **ascending order**, convert *it to a **height-balanced** binary search tree*.

A **height-balanced** binary tree is a binary tree in which the depth of the two subtrees of every node never differs by more than one.

**Example 1:**

![Convert%20Sorted%20Array%20to%20Binary%20Search%20Tree%20-%20LeetC%20dac73d59684f4317b091c8bebb70137e/btree1.jpg](Convert%20Sorted%20Array%20to%20Binary%20Search%20Tree%20-%20LeetC%20dac73d59684f4317b091c8bebb70137e/btree1.jpg)

```
Input: nums = [-10,-3,0,5,9]
Output: [0,-3,9,-10,null,5]
Explanation: [0,-10,5,null,-3,null,9] is also accepted:

```

![Convert%20Sorted%20Array%20to%20Binary%20Search%20Tree%20-%20LeetC%20dac73d59684f4317b091c8bebb70137e/btree2.jpg](Convert%20Sorted%20Array%20to%20Binary%20Search%20Tree%20-%20LeetC%20dac73d59684f4317b091c8bebb70137e/btree2.jpg)

**Example 2:**

```
Input: nums = [1,3]
Output: [3,1]
Explanation: [1,null,3] and [3,1] are both height-balanced BSTs.

```

**Constraints:**

- `1 <= nums.length <= 104`
- `104 <= nums[i] <= 104`
- `nums` is sorted in a **strictly increasing** order.

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    
    TreeNode* buildTheTree(vector<int> &nums, int s, int e){
        if(s>e) return NULL;
        
        int mid = (s + e)/2;
        
        TreeNode* head  = new TreeNode(nums[mid]);
        head->left = buildTheTree(nums, s, mid - 1);
        head->right = buildTheTree(nums, mid + 1, e);
        
        return head;
    }
    
    
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        
        return buildTheTree(nums, 0, nums.size() - 1);
        
    }
};
```