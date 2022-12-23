# Mother Vertex | Interviewbit

Created: July 27, 2022 11:52 PM
Tags: Graphs
URL: https://www.interviewbit.com/problems/mother-vertex/

**Problem Description**

You are given a directed graph with **A** vertices and **M** edges.
 You are given an array **B** with dimensions **M x 2**, where each row denotes a directed edge from Bi, 0 to Bi, 1.
 You need to find if there exists a mother vertex in the given graph. Return **1** if it exists, otherwise **0**.

A mother vertex is defined as a vertex from which all the vertices in the graph are accessible by a directed path.

**Problem Constraints**

1 <= A <= 105
 1 <= M <= 2 * 105
 1 <= Bi, 0, Bi, 1 <= A
 There can be duplicate edges or self loops in the input graph.

**Input Format**

The first argument is the integer A. The second argument is the 2D integer array B.

**Output Format**

**Example Input**

Input 1:

```
A = 3
B = [[1, 3], [2, 3], [1, 3]]

```

Input 2:

```
A = 3
B = [[1, 3], [2, 3], [3, 2]]

```

**Example Output**

Output 1:

```
0

```

Output 2:

```
1

```

**Example Explanation**

Explanation 1:

```
There is no vertex from which all the other vertices are accessible.
Note there can be duplicate edges.
```

Explanation 2:

```
Vertex 1 is the mother vertex. We can reach 2 using 1 -> 3 -> 2. We can reach 3 using 1 -> 3

```

Kosajural’s Algorithm

```cpp
vector<vector<int>>arr,trp;
int v;
vector<int>visited;
void dfs(int x)
{
    visited[x]=1;
    for(auto u:arr[x])
    {
        if(!visited[u])
            dfs(u);
    }
    v=x;
}
int Solution::motherVertex(int n, vector<vector<int> > &A) {
    arr.clear();
    trp.clear();
    v=0;visited.clear();
    arr.resize(n+1);
    trp.resize(n+1);
    visited.resize(n+1);
    int i;
    for(auto u:A)
    {
        arr[u[0]].push_back(u[1]);
        trp[u[1]].push_back(u[0]);
    }
    for(i=1;i<=n;i++)
    {
        if(!visited[i])dfs(i);
    }
    visited.clear();
    visited.resize(n+1);
    dfs(v);
    for(i=1;i<=n;i++)
    {
        if(!visited[i])return 0;
    }
    return 1;
}
```

Inefficient solution

```cpp
vector<vector<int>>arr,trp;
int v;
vector<int>visited;
void dfs(int x)
{
    visited[x]=1;
    for(auto u:arr[x])
    {
        if(!visited[u])
            dfs(u);
    }
    v=x;
}
int Solution::motherVertex(int n, vector<vector<int> > &A) {
    arr.clear();
    trp.clear();
    v=0;visited.clear();
    arr.resize(n+1);
    trp.resize(n+1);
    visited.resize(n+1);
    int i;
    for(auto u:A)
    {
        arr[u[0]].push_back(u[1]);
        trp[u[1]].push_back(u[0]);
    }
    for(i=1;i<=n;i++)
    {
        if(!visited[i])dfs(i);
    }
    visited.clear();
    visited.resize(n+1);
    dfs(v);
    for(i=1;i<=n;i++)
    {
        if(!visited[i])return 0;
    }
    return 1;
}
```