# Black Shapes | Interviewbit

Created: July 30, 2022 2:25 AM
Tags: BFS, Graphs
URL: https://www.interviewbit.com/problems/black-shapes/

Given **N x M** character matrix **A** of `O's` and `X's`, where `O` = `white`, `X` = `black`.

Return the number of black shapes. A black shape consists of one or more adjacent `X's` (diagonals not included)

**Input Format:**

```
    The First and only argument is a N x M character matrix.

```

**Output Format:**

```
    Return a single integer denoting number of black shapes.

```

**Constraints:**

```
    1 <= N,M <= 1000
    A[i][j] = 'X' or 'O'

```

**Example:**

```
Input 1:
    A = [ OOOXOOO
          OOXXOXO
          OXOOOXO  ]
Output 1:
    3
Explanation:
    3 shapes are  :
    (i)    X
         X X
    (ii)
          X
    (iii)
          X
          X

```

**Note:** we are looking for connected shapes here.

```
XXX
XXX
XXX

```

is just **one** single connected black shape.

```cpp
int Solution::black(vector<string> &A) {
    int r = A.size(); // rows in the array
    int c = A[0].length(); // columns in the array
    vector<vector<bool>> visi(r, vector<bool>(c, false)); // visited array
    
    
    // for finding the neigbours of an element
    int dx[] = {0,0,-1,1};  
    int dy[] = {1,-1,0,0};
    
    
    // Queue for BFS Traversal
    queue<pair<int, int>> q;
    
    int ans = 0;
    for(int i = 0; i<r; i++){  // for loop for going to each cell
        for(int j = 0; j<c; j++){
            
            if(A[i][j] == 'X' and visi[i][j] == false){ // if we get a call which is not visited and 
                                                        // the character is 'X' then doing BFS on it
                ans++;
                q.push({i, j});
                while(!q.empty()){
                    int x = q.front().first;
                    int y = q.front().second;
                    q.pop();
                    for(int k = 0; k<4; k++){
                        int newx = x + dx[k];
                        int newy = y + dy[k];
                        if(newx>=0 and newy>=0 and newx<r and newy <c and visi[newx][newy] == false and A[newx][newy] == 'X'){
                            visi[newx][newy] = true;
                            q.push({newx, newy});
                        }
                    }  
                }
            }
        }
    }
    return ans;
}
```