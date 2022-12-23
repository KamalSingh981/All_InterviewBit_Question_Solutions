# Path in Matrix | Interviewbit

Created: July 27, 2022 10:25 PM
Tags: BinarySearchTree, Graphs
URL: https://www.interviewbit.com/problems/path-in-matrix/

**Problem Description**

Given **N x N** matrix filled with **0**, **1**, **2**, **3**.
 Find whether there is a path possible from source to destination, traversing through blank cells only. 
 You can traverse up, down, right, and left. Return a single integer **1** if a path exists, otherwise **0**.

- A value of cell 1 means Source.
- A value of cell 2 means Destination.
- A value of cell 3 means Blank cell.
- A value of cell 0 means Blank Wall.

**Note**: there are an only a single source and single destination(sink).

**Problem Constraints**

**Input Format**

**Output Format**

Return a single integer **1** if a path exists, otherwise **0**.

**Example Input**

Input 1:

```
A = [[1, 0], [0, 2]]

```

Input 2:

```
A = [[1, 3], [3, 2]]

```

**Example Output**

Output 1:

```
0

```

Output 2:

```
1

```

**Example Explanation**

Explanation 1:

```
The source is blocked by walls on all its sides. So, there is no way to reach the destination.
```

Explanation 2:

```
We can take any possible path to reach the destination from the source.

```

```cpp
int Solution::checkPath(vector<vector<int> > &A) {
    int r = A.size();
    int c = A[0].size();
    
    int dx[] = {1,-1,0,0};
    int dy[] = {0,0,1,-1};
    
    pair<int, int> source;
    
    // finding the source
    for(int i = 0; i<r; i++){
        for(int j = 0; j<c; j++){
            if(A[i][j] == 1){
                source.first = i; // indexing is 0 base
                source.second = j;
            }
        }
    } 

    
    
    queue<pair<int, int>> q;
    q.push(source);
    map<pair<int, int>, bool> m;
    while(!q.empty()){
        int  x = q.front().first;
        int  y = q.front().second;
        q.pop();
        
        // if we reach to the destination
        if(A[x][y] == 2){
            return 1;
        }
        
        for(int i = 0; i<4; i++){
            int newx = x + dx[i];
            int newy = y + dy[i];
            if(newx>=0 and newx <c and newy >=0 and newy<r and m.find({newx, newy}) == m.end()){
                if(A[newx][newy] == 2){
                    return 1;
                }   
                else if(A[newx][newy] == 3){
                    q.push({newx, newy});
                    m[{newx, newy}] = true;
                }
                
            }
        }
    }
    return 0;
}
```

Inter view Code

```cpp
int Solution::checkPath(vector<vector<int> > &nums) {
    const int n = nums.size();
    int srcx, srcy, destx, desty;
    for(int i=0;i<n;i++){
        for(int j=0;j<n;j++){
            if (nums[i][j] == 1){
                srcx = i;
                srcy = j;
            }
            else if (nums[i][j] == 2){
                destx = i;
                desty = j;
            }
        }
    }

    int dx[4] = {-1, 0, 1, 0};
    int dy[4] = {0, 1, 0, -1};

    queue<pair<int,int>> pq;
    pq.push({srcx, srcy});
    while (!pq.empty()){
        auto node = pq.front();
        pq.pop();
        int x = node.first;
        int y = node.second;

        if (x == destx && y == desty){
            return 1;
        }

        for(int k=0;k<4;k++){
            int nx = x + dx[k];
            int ny = y + dy[k];

            if (nx >= 0 && ny >= 0 && nx < n && ny < n && nums[nx][ny] != 0){
                pq.push({nx, ny});
                nums[nx][ny] = 0;
            }
        }
    }
    return 0;
}
```