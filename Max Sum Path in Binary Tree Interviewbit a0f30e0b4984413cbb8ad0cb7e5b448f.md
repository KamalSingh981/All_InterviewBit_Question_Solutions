# Max Sum Path in Binary Tree | Interviewbit

Created: August 8, 2022 5:12 AM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/max-sum-path-in-binary-tree/

Given a binary tree **T**, find the maximum path sum.

The path may start and end at any node in the tree.

**Input Format:**

```
The first and the only argument contains a pointer to the root of T, A.

```

**Output Format:**

```
Return an integer representing the maximum sum path.

```

**Constraints:**

```
1 <= Number of Nodes <= 7e4
-1000 <= Value of Node in T <= 1000

```

**Example :**

```
Input 1:

       1
      / \
     2   3

Output 1:
     6

Explanation 1:
    The path with maximum sum is: 2 -> 1 -> 3

Input 2:

       -10
       /  \
     -20  -30

Output 2:
    -10

Explanation 2
    The path with maximum sum is: -10

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
 
 int findSolutionOfThisProblem(TreeNode*node, int &ans){
    if(node == NULL) return 0;
 
 
    int left = findSolutionOfThisProblem(node->left, ans);
    int right = findSolutionOfThisProblem(node->right, ans);
    
    int max_single = max(max(left, right) + node->val, node->val);
    int max_top = max(max_single, left + right + node->val);
    
    ans = max(max_top, ans);
    return max_single;
 
 }
 
 
int Solution::maxPathSum(TreeNode* A) {
    int ans = INT_MIN;
    findSolutionOfThisProblem(A, ans);
    return ans;
}
```