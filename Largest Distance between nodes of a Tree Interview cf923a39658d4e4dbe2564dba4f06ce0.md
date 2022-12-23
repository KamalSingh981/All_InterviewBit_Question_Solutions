# Largest Distance between nodes of a Tree | Interviewbit

Created: July 30, 2022 3:09 AM
Tags: Graphs
URL: https://www.interviewbit.com/problems/largest-distance-between-nodes-of-a-tree/

**Problem Description**

Given an arbitrary unweighted rooted tree which consists of **N** nodes.

The goal of the problem is to find **largest distance between two nodes in a tree.**

Distance between two nodes is a number of edges on a path between the nodes (there will be a unique path between any pair of nodes since it is a tree).

The nodes will be numbered **0** through **N - 1**.

The tree is given as an array **A**, there is an edge between nodes **A[i]** and **i (0 <= i < N)**. Exactly one of the i's will have A[i] equal to -1, it will be root node.

**Problem Constraints**

**Input Format**

First and only argument is an integer array A of size **N**.

**Output Format**

Return a single integer denoting the largest distance between two nodes in a tree.

**Example Input**

**Example Output**

**Example Explanation**

Explanation 1:

```
 node 0 is the root and the whole tree looks like this:
          0
       /  |  \
      1   2   3
               \
                4

 One of the longest path is 1 -> 0 -> 3 -> 4 and its length is 3, thus the answer is 3.

```

```cpp
int computediameter(int root, int parent , map<int, vector<int>> &m, int &ans){
    int first_height = 0;
    int second_height = 0;
    int child_no = 0;
    
    for(auto i:m[root]){
        
        if(i != parent){
            child_no++;
            int height = computediameter(i, root, m, ans);
            
            if(first_height<height){
                second_height = first_height;
                first_height = height;
            }
            else if(second_height<height){
                second_height = height;
            }
        }
    }
    
    int temp = first_height + second_height;
    if(child_no>=2) temp = temp + 2;
    else if(child_no == 1) temp = temp + 1;
    
    ans = max(ans, temp);
    
    if(child_no>0){
        return first_height + 1;
    }
    else{
        return 0;
    }
}

int Solution::solve(vector<int> &A) {
    
    // find the size of node
    int n = A.size();
    
    // make bidirectional adjacency list and find root
    map<int, int> m;
    vector<bool> visited(n);
    int root;
    map<int, vector<int>> adj;
    for(int i=0; i<n; i++){
        if(A[i] == -1){
            root = i;
            continue;
        }
        
        int u = i;
        int v = A[i];
        adj[u].push_back(v);
        adj[v].push_back(u);
    }
    
    int ans = 0;
    // find diameter of tree
    computediameter(root, -1, adj, ans);
    
    return ans;
}
```

Interviewbit code

```cpp
int Solution::solve(vector<int> &A) {
     vector<int> hgt(A.size(),0);
    int ans=0,maxx=0;
    for(int i=A.size()-1;i>0;i--){
        ans=max(ans,hgt[A[i]]+hgt[i]+1);
        hgt[A[i]]=max(hgt[i]+1,hgt[A[i]]);
    }
    return ans;
}
```