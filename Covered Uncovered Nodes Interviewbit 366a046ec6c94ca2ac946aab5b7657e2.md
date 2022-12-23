# Covered / Uncovered Nodes | Interviewbit

Created: July 24, 2022 5:12 PM
Tags: Binary Trees
URL: https://www.interviewbit.com/problems/covered-uncovered-nodes/

**Problem Description**

You are given the root of a binary tree **A**, you need to return the absolute difference between sum of all covered elements and the sum of all uncovered elements.

In a binary tree, a node is called Uncovered if it appears either on left boundary or right boundary. Rest of the nodes are called covered.

**Problem Constraints**

**Input Format**

**Output Format**

Return a single integer denoting the absolute difference of the sum of covered and uncovered nodes.

**Example Input**

Input 1:

```
    2
   / \
  1   4
 /   / \
6  10   5

```

Input 2:

```
      1
     /
    2
   /
  3

```

**Example Output**

**Example Explanation**

Explanation 1:

```
The node with value 10 is the only covered node. All other nodes are uncovered.
Therefore, the absolute difference is |(10) - (2 + 1 + 4 + 6 + 5)| = 8
```

Explanation 2:

```
All the given nodes are uncovered. Hence, the answer is sum of given nodes - 6.

```

```cpp
long Solution::coveredNodes(TreeNode * A)
    {
        long sum1 = 0;
        long sum2 = 0;
        queue<TreeNode *> q;
        q.push(A);
        while (!q.empty())
        {
            int cnt = q.size();
            TreeNode *tem = q.front();
            q.pop();
            sum1 += tem->val;
            if (tem->left)
                q.push(tem->left);
            if (tem->right)
                q.push(tem->right);
            for (int i = 1; i < cnt - 1; i++)
            {
                tem = q.front();
                q.pop();
                sum2 += tem->val;
                if (tem->left)
                    q.push(tem->left);
                if (tem->right)
                    q.push(tem->right);
            }
            if (cnt != 1)
            {
                tem = q.front();
                q.pop();
                sum1 += tem->val;
                if (tem->left)
                    q.push(tem->left);
                if (tem->right)
                    q.push(tem->right);
            }
        }
        return abs(sum1 - sum2);
    }
```