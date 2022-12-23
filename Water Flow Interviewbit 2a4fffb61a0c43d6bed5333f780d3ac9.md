# Water Flow | Interviewbit

Created: July 29, 2022 2:55 AM
Tags: BFS, Graphs
URL: https://www.interviewbit.com/problems/water-flow/

**Problem Description**

Given an **N x M** matrix **A** of non-negative integers representing the **height** of each unit cell in a continent, the "Blue lake" touches the left and top edges of the matrix and the "Red lake" touches the right and bottom edges.

Water can only flow in four directions (up, down, left, or right) from a cell to another one with **height equal or lower**.

Find the number of cells from where water can flow to both the Blue and Red lake.

**Problem Constraints**

1 <= M, N <= 1000

1 <= A[i][j] <= 109

**Input Format**

First and only argument is a 2D matrix A.

**Output Format**

Return an integer denoting the number of cells from where water can flow to both the Blue and Red lake.

**Example Input**

Input 1:

```
 A = [
       [1, 2, 2, 3, 5]
       [3, 2, 3, 4, 4]
       [2, 4, 5, 3, 1]
       [6, 7, 1, 4, 5]
       [5, 1, 1, 2, 4]
     ]
```

Input 2:

```
 A = [
       [2, 2]
       [2, 2]
     ]

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 Blue Lake ~   ~   ~   ~   ~
        ~  1   2   2   3  (5) *
        ~  3   2   3  (4) (4) *
        ~  2   4  (5)  3   1  *
        ~ (6) (7)  1   4   5  *
        ~ (5)  1   1   2   4  *
           *   *   *   *   * Red Lake
 Water can flow to both lakes from the cells denoted in parentheses.

```

Explanation 2:

```
 Water can flow from all cells.
```

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
int dx[4] = {1, -1, 0, 0};
int dy[4] = {0, 0, -1, 1};

void bfs(vector<vector<int>> &a, vector<vector<bool>> &vis, queue<pair<int, int>> q, int r, int c){
    while(!q.empty()){
        int x = q.front().first;
        int y = q.front().second;
        
        q.pop();
        for(int i = 0; i<4; i++){
            int newx = x + dx[i];
            int newy = y + dy[i];
            
            if(newx >=0 and newy >=0 and newx < r and newy <c and  vis[newx][newy] == false and a[x][y] <= a[newx][newy]){
                q.push({newx, newy});
                vis[newx][newy] = true;
            }       
        }
    }
}

int Solution::solve(vector<vector<int> > &A) {
    int row = A.size();
    if(row== 0){
        return 0;
    }
    int column = A[0].size();
    
    
    vector<vector<bool>> blue_lake(row, vector<bool>(column, false));
    vector<vector<bool>> red_lake(row, vector<bool>(column, false));
    
    queue<pair<int, int>> blue, red;
    
    
    for(int i  = 0; i<row; i++){
        for(int j = 0; j<column; j++){
            if(i == 0 || j == 0){
                blue.push({i, j});
                blue_lake[i][j] = true;
            }
            if(i == row - 1 || column -1 == j){
                red.push({i, j});
                red_lake[i][j] = true;
            }
        }
    }
    
    // Calling bfs function from both sides
    bfs(A, blue_lake, blue, row, column);
    bfs(A, red_lake, red, row, column);
    
    
    int ans = 0;
    for(int i= 0; i<row; i++){
        for(int j = 0; j<column; j++){
            if(blue_lake[i][j]  and red_lake[i][j]){
                ans++;
            }
        }
    }
    return ans;
}
```