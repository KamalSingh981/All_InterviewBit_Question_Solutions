# Cycle in Directed Graph | Interviewbit

Created: July 28, 2022 11:35 PM
Tags: DFS, Graphs
URL: https://www.interviewbit.com/problems/cycle-in-directed-graph/

**Problem Description**

Given an directed graph having **A** nodes. A matrix **B** of size `M x 2` is given which represents the **M** edges such that there is a edge directed from node **B[i][0]** to node **B[i][1]**.

Find whether the graph contains a cycle or not, return **1** if cycle is present else return **0**.

**NOTE:**

- The cycle must contain atleast two nodes.
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

*Return **1** if cycle is present else return **0**.*

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
 The given graph contain cycle 1 -> 3 -> 4 -> 1 or the cycle 1 -> 2 -> 4 -> 1

```

Explanation 2:

```
 The given graph doesn't contain any cycle.

```

```cpp
bool help(int node, vector<int> &vis, vector<int> &stack, map<int, vector<int>> &edge){
    // visit node
    vis[node] = 1;
    stack[node] = 1;
    
    for(auto nbr:edge[node]){
        //two cases
        if(vis[nbr] == 0){
            bool cycle = help(nbr, vis, stack, edge);
            if(cycle){
                return  true;
            }
        }
        else if(stack[nbr] == 1){
            return true;
        }
        
    }  
    stack[node] = 0;
    return false;    
}

int Solution::solve(int A, vector<vector<int> > &B) {
    map<int, vector<int>> edge;
    for(auto i:B){
        edge[i[0]].push_back(i[1]);
        i.clear();
    }
    vector<int> stack(A+1, 0);
    vector<int> vis(A+1, 0);
    
    
    for(int  i = 1; i<=A; i++){
        if(help(i, vis, stack, edge)){
            return true;
        }
    }
    return false;
}
```