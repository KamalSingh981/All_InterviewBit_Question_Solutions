# Max edge queries! | Interviewbit

Created: August 6, 2022 3:15 AM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/max-edge-queries/

**Problem Description**

Given a tree with **N** nodes numbered from **1** to **N**.

Each edge is bi-directional and has a certain weight assigned to it.

You are given **Q** queries, in each query you are given two integers **u** and **v** and you are required to find the **maximum weighted edge** in a simple path from **u** to **v**.

You have to return the weight of the edge for each queries.

**Problem Constraints**

2 <= N, Q <= 105

1 <= u, v <= N and u != v

1 <= weight of any edge <= 108

**Input Format**

First argument is a 2-D array **A** of size **(N-1) x 3** where **(A[i][0], A[i][1])** denotes an edge of the tree from node **A[i][0]** to node **A[i][1]** with weight **A[i][2]**.

Second argument is a 2-D array **B** of size **Q x 2** denoting the queries, **B[i][0]** denotes u and **B[i][1]** denotes v.

**Output Format**

Return an integer array of size **Q** denoting the answer for each queries.

**Example Input**

Input 1:

```
 A = [  [1, 2, 11]
        [1, 3, 1]
        [2, 4, 12]
        [2, 5, 100]
     ]
 B = [  [3, 5]
        [2, 3]
     ]

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 Query 1: u  = 3 and v = 5 so edge (2 -> 5) is the maximum weighted in the path from u to v so we will return the
 edge weight as the answer for this query.
 Query 2: u = 2 and  v= 3 so edge (2 -> 1) is the maximum weighted in the path from u to v so we will return the
 edge weight as the answer for this query.

```

```cpp
const int N = 1e5+4;

vector<pair<int,int>> graph[N];

int par[32][N];

int mx[32][N];

int n;

int depth[N];

void dfs(int node, int p, int h)

{

    par[0][node] = p;

    depth[node] = h;

    for(auto [to, wt] : graph[node])

    {

        if(to == p) continue;

        mx[0][to] = wt;

        dfs(to, node, h+1);

    }

}

int get(int a, int b)

{

    if(a == b)

    return 0;

    if(depth[a] > depth[b]) swap(a, b);

    int gap = depth[b] - depth[a];

    int ans = 0;

    for(int bit = 0; bit<32; bit++)

    {

        if((1<<bit) & gap)

        {

            ans = max(ans, mx[bit][b]);

            b = par[bit][b];

        }

    }

    if(a == b)  // if a and b become equal no need to lift further just return ans

    return ans;

    for(int i = 31; i>=0; i--)

    {

        if(par[i][a] == par[i][b]) continue;

        ans = max({ans, mx[i][a], mx[i][b]});

        a = par[i][a];

        b = par[i][b];

    }

    // here they will be unequal just need lift of 1. So here we are considering that edge too.

    ans = max({ans, mx[0][a], mx[0][b]});

    return ans;

}

vector<int> Solution::solve(vector<vector<int> > &edges, vector<vector<int> > &q) {

    n = edges.size()+1;

    memset(par, -1, sizeof(par));

    memset(mx, 0, sizeof(mx));

    for(int i = 0; i<N; i++) graph[i].clear(), depth[i] = 0;

    for(int i = 0; i<edges.size(); i++)

    {

        graph[edges[i][0]].push_back({edges[i][1], edges[i][2]});

        graph[edges[i][1]].push_back({edges[i][0], edges[i][2]});

    }

    dfs(1, -1, 0);

    for(int b = 1; b<32; b++)

    {

        for(int node = 1; node <= n; node++)

        {

            int p = par[b-1][node];

            if(p != -1)

            {

                par[b][node] = par[b-1][p];

                mx[b][node] = max(mx[b-1][node], mx[b-1][p]);

            }

        }

    }

    vector<int> ans;

    for(int i = 0; i<q.size(); i++)

    {

        int a = q[i][0], b = q[i][1];

        ans.push_back(get(a, b));

    }

    return ans;

}
```