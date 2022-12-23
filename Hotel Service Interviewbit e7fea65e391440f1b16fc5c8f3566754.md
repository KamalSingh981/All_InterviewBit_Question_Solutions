# Hotel Service | Interviewbit

Created: August 10, 2022 2:27 AM
Tags: BFS, Queue
URL: https://www.interviewbit.com/problems/hotel-service/

**Problem Description**

You are travelling to Neverland. After a long journey, you decided to take rest in a hotel for a night.
 You have the map of Neverland in the form of 2D matrix **A** with dimensions **N x M**. 
 The rows are numbered from 1 to N, and the columns are numbered from 1 to M.
 You can travel from one cell to any adjacent cell. Two cells are considered adjacent if they share a side.
 In the map, there are only two digits, **0** and **1**, where **1** denotes a hotel in that cell, and **0** denotes an empty cell.

You are also given another 2D array B with dimension **Q x 2**,
 where each row denotes a co-ordinate (X, Y) on the map (1 - indexed). For each coordinate you have to find the distance to the nearest hotel.
 Return an array denoting the answer to each coordinate in the array B.

- *Problem Constraints**

1 <= N, M <= 103
 1 <= Q <= 105
 0 <= A[i][j] <= 1
 0 <= B[i][0] < N
 0 <= B[i][1] < M
 There is guranteed to be atleast one hotel on the map.

- *Input Format**

The first argument is the 2D integer array A.
 The second argument is the 2D integer array B.

- *Output Format**
- *Example Input**

Input 1:

```
A = [[0, 0],
     [1, 0]]
B = [[1, 1],
     [2, 1],
     [1, 2]]

```

Input 2:

```
A = [[1, 0, 0 1]]
B = [[1, 2],
     [1, 3]]

```

- *Example Output**

Output 1:

```
[1, 0, 2]

```

Output 2:

```
[1, 1]

```

- *Example Explanation**

Explanation 1:

```
(1, 1) is adjacent to a hotel. (2, 1) has a hotel. (1, 2) is two cells away from the hotel on (2, 1).
```

Explanation 2:

```
(1, 2) is adjacent to a hotel on (1, 1). (1, 3) is adjacent to a hotel on (1, 4).

```

```cpp
vector<int> Solution::nearestHotel(vector<vector<int> > &A, vector<vector<int> > &B) {
    
    // since in the question it is given that we can move to tha adjacent cell
    // for that these array are there
    int dx[4] = {0,0,1,-1};
    int dy[4] = {1,-1,0,0};
    
    // finding the row and column size of given matrix
    int n = A.size();
    int m = A[0].size();
    
    // creating the distance matrix for precalculating the shortest 
    // distance from the hotel to other coordinate
    
    // Also will be used as visited matrix for finding whether the cell is visited or not
    vector<vector<int>> dis(n, vector<int>(m, -1));
    
    
    // queue for mulitsource BFS
    queue<pair<pair<int, int>, int>> q;

    for(int i = 0; i<n; i++){
        for(int j = 0; j<m; j++){
            if(A[i][j] == 1){ // if we are at the hotal than 
             q.push({{i, j}, 0});  // push it in the queue and update the distance as 0
             dis[i][j] = 0; 
            }
        }  
    }
    
    while(!q.empty()){
        int x = q.front().first.first;
        int y = q.front().first.second;
        int d = q.front().second;
        q.pop();
        
        for(int i = 0; i<4; i++){
            int newx = x + dx[i];
            int newy = y + dy[i];
            // if the adjacent exits and it is not visited than push is in the queue and update the distance
            if(newx >=0 and newy >=0 and newx <n and newy < m and dis[newx][newy] == -1){
                q.push({{newx, newy}, d + 1});
                dis[newx][newy] = d + 1;    
            }
        }    
    }
    
    vector<int> ans(B.size());
    
    
    //  store all the distance in the ans array
    for(int i = 0; i<B.size(); i++){
        ans[i] = dis[B[i][0] - 1][B[i][1] - 1];
    }
    
    return ans;
}
```

Brute Force

```cpp
int fun(int x,int y,vector<vector<int>>&A, vector<pair<int, int>> &q){
    int ans=INT_MAX;

        for(auto s:q){
            pair<int,int>p=s;
            int a=p.first;int b=p.second;
            int anss=abs(x-a)+abs(y-b);
            ans=min(anss,ans);
        }

return ans;

}
vector<int> Solution::nearestHotel(vector<vector<int> > &A, vector<vector<int> > &B) {
    vector<int>v;
    vector<pair<int,int>>s;
    for(int i=0;i<A.size();i++){
        for(int j=0;j<A[i].size();j++){
            if(A[i][j]==1){
                pair<int ,int>x;
                x.first=i;
                x.second=j;
                s.push_back(x);
            }
        }
    }
    for(int i=0;i<B.size();i++){
        int x=B[i][0]-1;
        int y=B[i][1]-1;
        int ans=fun(x,y,A, s);
        v.push_back(ans);
    }
    
    return v;
}
```