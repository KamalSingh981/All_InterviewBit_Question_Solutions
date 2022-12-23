# Path with good nodes! | Interviewbit

Created: July 28, 2022 12:52 AM
Tags: DFS, Graphs
URL: https://www.interviewbit.com/problems/path-with-good-nodes/

**Problem Description**

Given a tree with **N** nodes labelled from **1** to **N**.

Each node is either **good** or **bad** denoted by binary array **A** of size **N** where if **A[i]** is **1** then **ithnode** is **good** else if **A[i]** is **0** then **ith** node is **bad**.

Also the given tree is rooted at node **1** and you need to tell the number of **root to leaf** paths in the tree that contain not more than **C** good nodes.

**NOTE:**

- Each edge in the tree is **bi-directional**.

**Problem Constraints**

2 <= N <= 105

A[i] = 0 or A[i] = 1

0 <= C <= N

**Input Format**

First argument is an binary integer array **A** of size **N**.

Second argument is a 2-D array **B** of size **(N-1) x 2** denoting the edge of the tree.

Third argument is an integer **C**.

**Output Format**

Return an integer denoting the number of **root to leaf** paths in the tree that contain not more than **C** good nodes.

**Example Input**

Input 1:

```
 A = [0, 1, 0, 1, 1, 1]
 B = [  [1, 2]
        [1, 5]
        [1, 6]
        [2, 3]
        [2, 4]
     ]
 C = 1

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 Path (1 - 2 - 3) and (1 - 5) and (1 - 6) are the paths which contain atmost C nodes.

```

```cpp
void dfs(int src,int parent,int goodnodes, vector<int>&A, map<int, vector<int>> &m, int & C, int &ans){
    // Increment if good Nodes
    if(A[src - 1] == 1) goodnodes++;
    //if good nodes exceeds  the limit
    if(goodnodes>C) return;
    
    int count_of_child = 0;
    //explore it's  count_of_child
    for(int child:m[src]){
        if(child!=parent){
            count_of_child++;
            // call the dfs for its child
            dfs(child,src, goodnodes, A, m,C, ans);
        }
    }
    
    // if we reach at leaf nodes
    if(count_of_child == 0){
        ans++;
    }
}

int Solution::solve(vector<int> &A, vector<vector<int> > &B, int C) {
    
    map<int, vector<int>> m;
    vector<bool> v(A.size() + 1);
    for(auto i :v){
        i = false;
    }
    for(auto i:B){
        m[i[0]].push_back(i[1]); 
        m[i[1]].push_back(i[0]);
    }
    
    int ans = 0;
```