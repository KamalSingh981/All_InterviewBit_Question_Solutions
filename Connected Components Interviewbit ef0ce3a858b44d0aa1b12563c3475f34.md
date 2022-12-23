# Connected Components | Interviewbit

Created: July 27, 2022 12:14 AM
Tags: Graphs
URL: https://www.interviewbit.com/problems/connected-components/

**Problem Description**

Given a graph with **A** nodes.
The edges in graph are given in a 2D array **B**.
There is an undirected edge between **B[i][0]** and **B[i][1]**.
Find the **number of connected components** in the given graph.

**Problem Constraints**

1 <= A <= 105
1 <= |B| <= 105
1 <= B[i][0], B[i][1] <= A

**Input Format**

First argument is an integer A.
Second argument is a 2D integer array B.

**Output Format**

**Example Input**

Input 1:

```
A = 4
B = [[1, 2],
     [2, 3]]

```

Input 2:

```
A = 3
B = [1, 2]
    [2, 1]

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 The two connected components are [1, 2, 3] and [4].

```

Explanation 2:

```
The two connected components are [1, 2] and [3].

```

```cpp
const int N =100005;
vector<int> adj[N], visited(N);

void clean(int n){
    for(int i=0; i<=n; ++i){
        adj[i].clear();
        visited[i]=0;
    }
}

void addEdge(int u, int v){
    adj[u].push_back(v);
    adj[v].push_back(u);
}

void DFSRec(int s){
    visited[s] = 1;
    for(int u: adj[s]){
        if(visited[u]==0) DFSRec(u);
    }
}

int Solution::solve(int A, vector<vector<int> > &B) {
    clean(A);
    for(int i = 0; i <B.size(); i++){
        addEdge(B[i][0], B[i][1]);
    }
    int count = 0;
    for(int i = 1; i<=A; i++){
        if(visited[i]==0){
            DFSRec(i);
            count++;
        }
    }
    return count;
}
```