# Path in Directed Graph | Interviewbit

Created: July 26, 2022 3:24 PM
Tags: BFS, Graphs
URL: https://www.interviewbit.com/problems/path-in-directed-graph/

**Problem Description**

Given an directed graph having **A** nodes labelled from **1** to **A** containing **M** edges given by matrix **B** of size `M x 2`such that there is a edge directed from node

**B[i][0]** to node **B[i][1]**.

Find whether a path exists from node **1** to node **A**.

Return **1** if path exists else return **0**.

**NOTE:**

- There are no self-loops in the graph.
- There are no multiple edges between two nodes.
- The graph may or may not be connected.
- Nodes are numbered from 1 to A.
- Your solution will run on multiple test cases. If you are using global variables make sure to clear them.

**Problem Constraints**

2 <= A <= 105

1 <= M <= min(200000,A*(A-1))*

*1 <= B[i][0], B[i][1] <= A*

*Input Format*

*The first argument given is an integer **A** representing the number of nodes in the graph.*

*The second argument given a matrix **B** of size `M x 2` which represents the **M** edges such that there is a edge directed from node **B[i][0]** to node **B[i][1]**.*

*Output Format*

*Return **1** if path exists between node **1** to node **A** else return **0**.*

*Example Input*

*Input 1: 

 `A = 5
 B = [  [1, 2] 
        [4, 1] 
        [2, 4] 
        [3, 4] 
        [5, 2] 
        [1, 3] ]`
 
Input 2: 

 `A = 5
 B = [  [1, 2]
        [2, 3] 
        [3, 4] 
        [4, 5] ]`*

*Example Output*

*Example Explanation*

- 

Explanation 1:

```
 The given doens't contain any path from node 1 to node 5 so we will return 0.

```

Explanation 2:

```
 Path from node1 to node 5 is ( 1 -> 2 -> 3 -> 4 -> 5 ) so we will return 1.

```

```cpp
int Solution::solve(int A, vector<vector<int> > &B) {
    map<int, bool> visited;
    map<int, vector<int>> m;
    for(int i = 0; i<B.size(); i++){
        m[B[i][0]].push_back(B[i][1]);
    }
    for(int i = 1; i<=A; i++){
        visited[i] = false;
    }
    queue<int> q;
    q.push(B[0][0]);
    visited[B[0][0]] = true;
    while(!q.empty()){
        int temp = q.front();
        if(temp == A){
            return 1;
        }
        q.pop();
        for(auto i:m[temp]){
            
            if(visited[i] == false){
                q.push(i);
                visited[i] = true;
            }
        }
    }   
    return 0;
}
```