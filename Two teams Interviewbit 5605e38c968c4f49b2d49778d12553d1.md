# Two teams? | Interviewbit

Created: July 29, 2022 2:08 AM
Tags: Biparted, Graphs
URL: https://www.interviewbit.com/problems/two-teams/

**Problem Description**

There are **A** people numbered 1 to A in a football academy.
 The coach of the academy wants to make two teams (not necessary of equal size) but unfortunately, not all people get along, and several refuse to be put on the same team as that of their enemies.

Given a 2-D array **B** of size `M x 2` denoting the enemies i.e B[i][0] and B[i][1] both are enemies of each other.

Return **1** if it possible to make exactly two teams else return **0**.

**Problem Constraints**

2 <= A <= 105

1 <= M <= 105

1 <= B[i][0], B[i][1] <= A

B[i][0] != B[i][1]

**Input Format**

First argument is an integer A denoting number of peoples.

Second argument is a 2-D array B of size M x 2 denoting enemies.

**Output Format**

Return **1** if it possible to make exactly two teams else return **0**.

**Example Input**

Input 1:

```
 A = 5
 B = [ [1, 2],
       [2, 3],
       [1, 5],
       [2, 4] ]
```

Input 2:

```
 A = 4
 B = [ [1, 4],
       [3, 1],
       [4, 3],
       [2, 1] ]

```

**Example Output**

Output 1:

```
 1
```

Output 2:

```
 0
```

**Example Explanation**

Explanation 1:

```
 We can make two teams [1, 3, 4] and [2, 5].
```

Explanation 2:

```
 No possible way to create two teams. So, we need to return 0.
```

```cpp
bool dfs_helper(map<int, vector<int>> &edge, int node, int parent, vector<int> &visited, int color){
    // color the node    
    visited[node] = color;
    
    
    for(auto nbr: edge[node]){
        if(visited[nbr] == 0){
            int subprob = dfs_helper(edge, nbr, node, visited, 3 - color);
            if(subprob == false){
                return false;
            }
        }
        
        else if(nbr != parent and color == visited[nbr]){
            return false;
        }
    }
    return true;
}

int Solution::solve(int A, vector<vector<int> > &B) {
    
    map<int, vector<int>> edge;
    for(auto i:B){
        edge[i[0]].push_back(i[1]);
        edge[i[1]].push_back(i[0]);
    }
    
    vector<int> visited(A +1, 0);
    
    for(int  i = 1; i<= A; i++){
        if(visited[i] == 0){ 
            bool ans = dfs_helper(edge, i, -1, visited, 1);
            if(ans == false){
                return false;
            }
        }
    }
    return true;
}
```