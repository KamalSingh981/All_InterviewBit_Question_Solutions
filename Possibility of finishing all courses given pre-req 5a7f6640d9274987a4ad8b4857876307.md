# Possibility of finishing all courses given pre-requisites | Interviewbit

Created: July 30, 2022 1:36 AM
Tags: Graphs
URL: https://www.interviewbit.com/problems/possibility-of-finishing-all-courses-given-prerequisites/

**Problem Description**

There are a total of **A** courses you have to take, labeled from **1** to **A**.
Some courses may have prerequisites, for example to take course **2** you have to first take course **1**, which is expressed as a pair: **[1,2]**.
The pairs are given as two arrays B and C, where [B[i], C[i]] form a pair.

Given the total number of courses and a list of prerequisite pairs, is it possible for you to finish all courses?
Return **1** if it is **possible** to finish all the courses, or **0** if it is **not possible** to finish all the courses.

**Problem Constraints**

1 <= A <= 64
1 <= length(B) = length(C) <= 1e5
1 <= B[i], C[i] <= A

**Input Format**

The first argument of input contains an integer A, representing the number of courses.
The second argument of input contains an integer array, B.
The third argument of input contains an integer array, C.

**Output Format**

Return a boolean value:
 1 : If it is possible to complete all the courses.
 0 : If it is not possible to complete all the courses.

**Example Input**

Input 1:

```
A = 3
B = [1, 2]
C = [2, 3]

```

Input 2:

```
A = 2
B = [1, 2]
C = [2, 1]

```

**Example Output**

**Example Explanation**

Explanation 1:

```
It is possible to complete the courses in the following order:
1 -> 2 -> 3

```

Explanation 2:

```
It is not possible to complete all the courses.

```

```cpp
int Solution::solve(int A, vector<int> &B, vector<int> &C) {
    
    map<int, vector<int>> adj;
    vector<bool> visited(A+1, false);
    vector<int> indegree(A+1, 0);
    for(int  i= 0; i<B.size(); i++){
        adj[B[i]].push_back(C[i]);
        indegree[C[i]]++;
    }
    
    queue<int> q;
    int count = 0;
    for(int i = 1; i<= A; i++){
        if(indegree[i] == 0){
            q.push(i);
            visited[i] = true;
            count++;
        }
    }
    
    while(!q.empty()){
        int temp = q.front();
        q.pop();
        
        for(auto i:adj[temp]){
            if(!visited[i]){
                indegree[i]--;
                if(indegree[i] == 0){
                    q.push(i);
                    visited[i] = true;
                    count++;
                }
            }
        }
    }
    
    if(count == A)return 1;
    return 0;
}
```