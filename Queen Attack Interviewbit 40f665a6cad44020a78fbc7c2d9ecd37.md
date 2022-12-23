# Queen Attack | Interviewbit

Created: August 5, 2022 2:13 AM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/queen-attack/

On a **N * M** chessboard, where rows are numbered from 1 to N and columns from 1 to M, there are queens at some cells. Return a **N * M** array A, where A[i][j] is number of queens that can attack cell (i, j). While calculating answer for cell (i, j), assume there is no queen at that cell.

**Notes:**

1. Queen is able to move any number of squares vertically, horizontally or diagonally on a chessboard. A queen cannot jump over another queen to attack a position.
2. You are given an array of N strings, each of size M. Each character is either a `1` or `0` denoting if there is a queen at that position or not, respectively.
3. Expected time complexity is worst case O(N*M).

**For example**,

```
Let chessboard be,
[0 1 0]
[1 0 0]
[0 0 1]

where a 1 denotes a queen at that position.

Cell (1, 1) is attacked by queens at (2, 1), (1,2) and (3,3).
Cell (1, 2) is attacked by queen at (2, 1). Note that while calculating this, we assume that there is no queen at (1, 2).
Cell (1, 3) is attacked by queens at (3, 3) and (1, 2).
and so on...

Finally, we return matrix
[3, 1, 2]
[1, 3, 3]
[2, 3, 0]

```

```cpp
int dx[8]={-1,-1,0,1,1,1,0,-1};
int dy[8]={0,1,1,1,0,-1,-1,-1};

void Attack(int i, int j, vector<vector<int>> &ans, int n, int m, vector<string> &A){
    
    for(int k = 0; k<8; k++){
        int p = i + dx[k], q = j + dy[k];
        bool flag = true;
        while(p>=0 and q>=0 and p < n and q < m and flag){
            ans[p][q]++;
            if(A[p][q] == '1'){
                flag = false;
            }
            p += dx[k];
            q += dy[k];
        }
    }
}

vector<vector<int> > Solution::queenAttack(vector<string> &A) {
    int  n = A.size();
    int m = A[0].size();
    
    vector<vector<int>> ans(A.size(), vector<int>(A[0].size(), 0));
    
    
    for(int i = 0; i<n; i++){
        for(int j = 0; j<m; j++){
            if(A[i][j] == '1')
            Attack(i, j, ans, n, m, A);
        }
    }
    
    return ans;
}
```

Optimized Solution

```cpp
bool is_valid(int x,int y,int n,int m)
{
    if(x>=0 && x<n && y>=0 && y<m)
    {
        return true;
    }
    return false;
}

int my_rec(vector<vector<vector<int>>> &dp,vector<pair<int,int>> &dirs,vector<string> &A,int i,int j,int n, int m,int k)
{
    if(dp[k][i][j]!=-1)
    {
        return dp[k][i][j];
    }
    int x = i + dirs[k].first;
    int y = j + dirs[k].second;
    dp[k][i][j] = 0;
    if(is_valid(x,y,n,m))
    {
        // if a queen is present at x,y; only she can attack as no queen can jump over any other queen
        if(A[x][y] == '1')
        {
            dp[k][i][j]++;
        }
        else
        {
            dp[k][i][j] = my_rec(dp,dirs,A,x,y,n,m,k);   
        }
        return dp[k][i][j];
    }
    return 0;
}

vector<vector<int> > Solution::queenAttack(vector<string> &A) 
{
    int n = A.size();
    int m = A[0].size();
    vector<pair<int,int>> dirs = {{1,0},{1,-1},{0,-1},{-1,-1},{-1,0},{-1,1},{0,1},{1,1}};
    vector<vector<vector<int>>> dp(8,vector<vector<int>>(n,vector<int>(m,-1)));
    // dp[k][i][j] is the no of queens that can attack the cell i,j from direction k
    vector<vector<int>> res(n,vector<int>(m,0));
    // res[i][j] is the number of queens that can attck cell i,j from all dirn
    for(int k=0;k<8;k++)
    {
        for(int i=0;i<n;i++)
        {
            for(int j=0;j<m;j++)
            {
                res[i][j] += my_rec(dp,dirs,A,i,j,n,m,k); // we add it for all dirns
            }
        }
    }
    return res;
}
```