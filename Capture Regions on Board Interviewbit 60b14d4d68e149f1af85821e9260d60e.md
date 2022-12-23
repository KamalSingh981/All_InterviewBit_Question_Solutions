# Capture Regions on Board | Interviewbit

Created: July 29, 2022 3:05 PM
URL: https://www.interviewbit.com/problems/capture-regions-on-board/

**Problem Description**

Given a 2D character matrix **A** of size `N x M`, containing `'X'` and `'O'`, capture all regions surrounded by `'X'`.

A region is captured by flipping all `'O'`s into `'X'`s in that surrounded region.

**Problem Constraints**

**Input Format**

First and only argument 2D character matrix **A** of size `N X M`.

**Output Format**

Make changes to the the input only as matrix is passed by reference.

**Example Input**

Input 1:

```
 A = [  [X, X, X, X],
        [X, O, O, X],
        [X, X, O, X],
        [X, O, X, X]
     ]

```

**Example Output**

Output 1:

```
 A = [  [X, X, X, X],
        [X, X, X, X],
        [X, X, X, X],
        [X, O, X, X]
     ]

```

**Example Explanation**

Explanation 1:

```
 'O' in (4,2) is not surrounded by X from below.

```

```cpp
void Solution::solve(vector<vector<char> > &A) {
    // Do not write main() function.
    // Do not read input, instead use the arguments to the function.
    // Do not print the output, instead return values as specified
    // Still have a doubt. Checkout www.interviewbit.com/pages/sample_codes/ for more details
    
    
    int dx[] = {0,0,-1,1};
    int dy[] = {1,-1,0,0};
    
    queue<pair<int, int>> q;
    int r =  A.size();
    int c = A[0].size();
    for(int  i =0; i<r; i++){
        for(int j = 0; j<c; j++){
            if((j == 0 || i == 0 || i == r - 1 || j == c - 1) and A[i][j] == 'O'){
                q.push({i, j});
                A[i][j] = 'm';
            }
        }
    }
    
    while(!q.empty()){
        int x = q.front().first;
        int y = q.front().second;
        
        q.pop();
        
        for(int i =0; i<4; i++){
            int newx = x + dx[i];
            int newy = y + dy[i];
            
            if(newx>=0 and newy>=0 and newx < r and newy < c and A[newx][newy] == 'O'){
                q.push({newx, newy});
                A[newx][newy] = 'm';
            } 
        }  
    }
    
    for(int  i =0; i<r; i++){
        for(int j = 0; j<c; j++){
            if(A[i][j] == 'm'){
                A[i][j] = 'O';
            }
            else if(A[i][j] == 'O'){
                A[i][j] = 'X';
            }
        }
    }
}
```