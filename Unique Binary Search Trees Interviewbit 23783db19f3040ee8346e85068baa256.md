# Unique Binary Search Trees | Interviewbit

Created: July 26, 2022 9:22 PM
Tags: BinarySearchTree
URL: https://www.interviewbit.com/problems/unique-binary-search-trees/

Given **A**, generate all structurally unique BST’s (binary search trees) that store values **1…A**.

**Input Format:**

```
The first and the only argument of input contains the integer, A.

```

**Output Format:**

```
Return a list of tree nodes representing the generated BST's.

```

**Constraints:**

```
1 <= A <= 15

```

**Example:**

```
Input 1:
    A = 3

Output 1:

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3

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
 
void generate(vector<TreeNode* > &ret, int left, int right){
    if(left>right){
        return ret.push_back(NULL);
        return;
    }
    
    for(int i = left; i<= right; i++){
        vector<TreeNode* > lefts;
        generate(lefts, left, i - 1);
        
        vector<TreeNode* > rights;
        generate(rights, i+1, right);
        
        for(int u = 0; u<lefts.size(); u++){
            for(int v = 0; v<rights.size(); v++){
                TreeNode * root = new TreeNode(i);
                root->left = lefts[u];
                root->right = rights[v];
                ret.push_back(root);
            }
        }
    }
}

vector<TreeNode*> Solution::generateTrees(int A) {
    // Do not write main() function.
    // Do not read input, instead use the arguments to the function.
    // Do not print the output, instead return values as specified
    // Still have a doubt. Checkout www.interviewbit.com/pages/sample_codes/ for more details
    vector<TreeNode *> ret;
        generate(ret, 1, A);
        return ret;  
}
```