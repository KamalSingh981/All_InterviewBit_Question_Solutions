# Vertical Sum of a Binary Tree | Interviewbit

Created: July 24, 2022 4:33 PM
Tags: Binary Trees, Recursion
URL: https://www.interviewbit.com/problems/vertical-sum-of-a-binary-tree/

**Problem Description**

You are given the root of a binary tree **A**.
 You have to find the vertical sum of the tree.
 A vertical sum denotes an array of sum of the different verticals of a binary tree,
 where the leftmost vertical sum is the first element of the array and rightmost vertical is the last.

**Problem Constraints**

1 <= Number of nodes in the binary tree <= 105
 1 <= Ai <= 103

**Input Format**

**Output Format**

**Example Input**

Input 1:

```
A =     1
      /   \
     2     3
    / \   / \
   4   5 6   7

```

Input 2:

```
A =     1
       /
      2
     /
    3

```

**Example Output**

Output 1:

```
[4, 2, 12, 3, 7]

```

Output 2:

```
[3, 2, 1]

```

**Example Explanation**

Explanation 1:

```
The element 4 is present in the leftmost vertical.
The middle vertical consists of 3 elements 1, 5, 6.
The resultant array is [4, 2, 12, 3, 7].
```

Explanation 2:

```
The leftmost vertical is the element 3. The next verticals are 2 and 1.
Hence, the resultant array is [3, 2, 1].

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
 void mapping(TreeNode* root, map<int, int> &m, int d){
     if(root == NULL){
         return;
     }
     m[d] += root->val; 
     mapping(root->left, m, d-1);
     mapping(root->right, m, d+1);
 }
 
vector<int> Solution::verticalSum(TreeNode* A) {
    map<int, int> m;
    mapping(A, m, 0);
    vector<int> ans;
    for(auto i: m){
        ans.push_back(i.second);
    }
    return ans;
}
```