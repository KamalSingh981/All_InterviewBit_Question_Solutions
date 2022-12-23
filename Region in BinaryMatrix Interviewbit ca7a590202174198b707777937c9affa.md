# Region in BinaryMatrix | Interviewbit

Created: July 26, 2022 9:58 PM
Tags: BFS, Graphs
URL: https://www.interviewbit.com/problems/region-in-binarymatrix/

**Problem Description**

Given a binary matrix **A** of size `N x M`.

Cells which contain **1** are called **filled cell** and cell that contain **0** are called **empty cell**.

Two cells are said to be connected if they are adjacent to each other horizontally, vertically, or diagonally.

If one or more **filled cells** are also connected, they form a **region**. Find the **length of the largest region**.

**Problem Constraints**

1 <= N, M <= 102

A[i][j]=0 or A[i][j]=1

**Input Format**

First argument is a 2D binary matrix **A**of size  `N x M`.

**Output Format**

Return a single interger denoting the length of largest region.

**Example Input**

Input 1:

```
 A = [  [0, 0, 1, 1, 0]
        [1, 0, 1, 1, 0]
        [0, 1, 0, 0, 0]
        [0, 0, 0, 0, 1]
    ]

```

Input 2:

```
 A = [  [1, 1, 1]
        [0, 0, 1]
    ]

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 The largest region is denoted by red color in the matrix:
    00110
    10110
    01000
    00001

```

Explanation 2:

```
 The largest region is:
    111
    001

```

```cpp
int bfs(vector<vector<int>> &mat, int i, int j, int r, int c, int x[], int y[]){
    queue<pair<int, int>> q;
    int ans = 1;
    q.push({i, j});
    mat[i][j] = 0;
    while(!q.empty()){
        pair<int, int> temp = q.front();
        q.pop();
        for(int k = 0; k<8; k++){
            int a = temp.first + x[k], b = temp.second + y[k];
            if(a>=0 and b>=0 and a<r and b<c and mat[a][b] == 1){
                ans++;
                q.push({a,b});
                mat[a][b] = 0;
            }
        }
    }
    return ans;
}

void dfs(vector<vector<int> > &A,int i,int j,int &c,int r, int cl, int x[], int y[])
{
    c++;
    A[i][j]=0;
    int a,b;
    for(int k=0;k<8;k++)
    {
        a=i+x[k];
        b=j+y[k];
        if(a<0||a>=r||b<0||b>=cl)continue;
        if(A[a][b] == 0) continue;
        dfs(A,a,b, c, r, cl, x, y);
    }
}

int Solution::solve(vector<vector<int> > &A){
    int x[] = {1,1,1,-1,-1,-1,0,0};
    int y[] = {1,0,-1,1,0,-1,1,-1};
    
    int ans = 0;
    int r = A.size();
    int c = A[0].size();
    for(int i = 0; i<r; i++){
        for(int j = 0; j<c; j++){
            if(A[i][j] == 1){
                int count = 0;
                dfs(A, i, j, count,r, c, x, y);
                ans = max(ans, count);
            }
        }
    }
    return ans; 
}
```