# Useful Extra Edges | Interviewbit

Created: July 26, 2022 7:38 PM
Tags: Dijikstra's, Graphs
URL: https://www.interviewbit.com/problems/useful-extra-edges/

**Problem Description**

Given a graph of **A** nodes. Also given the weighted edges in the form of array **B**.

You are also given starting point **C** and destination point **D**.

Also given are some extra edges in the form of vector **E**.

You need to find the length of the shortest path from C to D if you can use maximum one road from the given roads in E.

All roads are bidirectional.

**Problem Constraints**

1 <= A <= 100000

1 <= |B| <= 100000

1 <= C, D <= A

1 <= |E| <= 300

All lengths of the roads lie between 1 and 1000.

**Input Format**

First argument is the integer A.

Second argument is the vector of vectors B.

Third argument is the integer C.

Fourth argument is the integer D.

Fifth argument is the vector of vectors E.

**Output Format**

Return -1 if C is not reachable from D. Else return the shortest distance between them.

**Example Input**

Input 1:

```
 A = 3
B = [   [1, 2, 1]
        [2, 3, 2]
    ]
C = 1
D = 3
E = [   [1, 3, 2]
    ]

```

Input 2:

```
 A = 4
B = [   [1, 2, 1]
        [2, 3, 2]
        [3, 1, 4]
    ]
C = 1
D = 4
E = [   [1, 3, 2]
    ]

```

**Example Output**

Output 1:

```
 2

```

Output 2:

```
 -1

```

**Example Explanation**

Explanation 1:

```
 Use the direct edge from 1 to 3. It has shortest path from 1 to 3.

```

Explanation 2:

```
 4 cannot be reached from 1.

```

```cpp
void dijistra_s(int src, vector<int> &dist, vector<pair<int, int>> adj[]){
    priority_queue<pair<int, int> , vector<pair<int, int>>, greater<pair<int, int>>> p;
    dist[src] = 0;
    
    p.push({0, src});
    while(!p.empty()){
        int dst = p.top().first;
        int node = p.top().second;
        p.pop();
        for(auto it: adj[node]){
            if(dist[it.first] > dist[node] + it.second){
                dist[it.first] = dist[node] + it.second;
                p.push({dist[it.first], it.first});
            }
        }
    }
}

int Solution::solve(int A, vector<vector<int> > &B, int C, int D, vector<vector<int> > &E) {
    
    vector<int> dist1(A+1, INT_MAX);
    vector<int> dist2(A+1, INT_MAX);
    vector<pair<int, int>> adj[A+1];
    
    for(int i = 0; i<B.size(); i++){
        adj[B[i][0]].push_back({B[i][1], B[i][2]});
        adj[B[i][1]].push_back({B[i][0], B[i][2]});
    }
    
    dijistra_s(C, dist1, adj);
    dijistra_s(D, dist2, adj);
    
    int ans = INT_MAX;
    if(dist1[D]!= INT_MAX) ans = dist1[D];
    for(int i = 0; i<E.size(); i++){
        if(dist1[E[i][0]] != INT_MAX and dist2[E[i][1]] != INT_MAX){
            ans=min({ans, dist1[E[i][0]]+dist2[E[i][1]]+E[i][2], dist1[E[i][1]]+dist2[E[i][0]]+E[i][2]});
        }
    }
    
    if(ans == INT_MAX){
        if(dist1[D] != INT_MAX) return dist1[D];
        return -1;
    }
    return ans;
}
```