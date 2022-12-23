# Delete Edge! | Interviewbit

Created: July 29, 2022 12:13 AM
Tags: Graphs
URL: https://www.interviewbit.com/problems/delete-edge/

**Problem Description**

Given a undirected tree with **N** nodes labeled from **1** to **N**.

Each node has a certain weight assigned to it given by an integer array **A** of size **N**.

You need to delete an edge in such a way that **Product** between sum of weight of nodes in one subtree with sum of weight of nodes in other subtree is **maximized**.

Return this maximum possible product modulo **109 + 7**.

**NOTE:**

- The tree is rooted at node labeled with 1.

**Problem Constraints**

2 <= N <= 105

1 <= A[i] <= 103

**Input Format**

First argument is an integer array **A** of size **N** denoting the weight of each node.

Second argument is a 2-D array **B** of size **(N-1) x 2** denoting the edge of the tree.

**Output Format**

Return a single integer denoting the maximum product prossible of sum of weights of nodes in the two subtrees formed by deleting an edge with modulo **109 + 7**.

**Example Input**

Input 1:

```
 A = [10, 5, 12, 6]
 B = [

        [1, 2]
        [1, 4]
        [4, 3]
     ]

```

Input 2:

```
 A = [11, 12]
 B = [

        [1, 2]
     ]

```

**Example Output**

Output 1:

```
 270
```

Output 2:

```
 132

```

**Example Explanation**

Explanation 1:

```
 Removing edge (1, 4) created two subtrees.
 Subtree-1 contains nodes (1, 2) and Subtree-2 contains nodes (3, 4)
 So product will be = (A[1] + A[2]) * (A[3] + A[4]) = 15 * 18 = 270

```

Explanation 2:

```
 Removing edge (1, 2) created two subtrees.
 Subtree-1 contains node (1) and Subtree-2 contains node (3)
 So product will be = (A[1]) * (A[2]) = 11 * 12 = 132

```

```cpp
vector<int> adj[100001];
int subtree_sum[100001],vis[100001];
int dfs(int node,vector<int> &v){
    vis[node]=1;
    int cnt=v[node-1];
    for(auto &child:adj[node]){
        if(!vis[child]){
            cnt+=dfs(child,v);
        }
    }
    return subtree_sum[node]=cnt;
}
int Solution::deleteEdge(vector<int> &v, vector<vector<int> > &edges) {
    int n=v.size();
    for(int i=1;i<=n;i++){
        adj[i].clear();
        subtree_sum[i]=0;
        vis[i]=0;
    }
    for(auto &e:edges){
        adj[e[1]].push_back(e[0]);
        adj[e[0]].push_back(e[1]);
    }
    dfs(1,v);
    long long ans=0,mod=1e9+7;
    for(int i=2;i<=n;i++){
        long long p1=subtree_sum[i],p2=subtree_sum[1]-p1;
        ans=max(ans,(p1*p2)%mod);
    }
    return ans;
}
```