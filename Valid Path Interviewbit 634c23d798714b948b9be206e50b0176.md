# Valid Path | Interviewbit

Created: July 26, 2022 8:07 PM
Tags: Graphs
URL: https://www.interviewbit.com/problems/valid-path/

There is a rectangle with left bottom as  `(0, 0)` and right up as `(x, y)`. There are `N circles` such that their centers are inside the `rectangle`.
 Radius of each circle is `R`. Now we need to find out if it is possible that we can move from `(0, 0)` to `(x, y)` without touching any `circle.`

**Note :**  We can move from any cell to any of its `8 adjecent neighbours` and we cannot move outside the boundary of the rectangle at any point of time.

**Input Format**

```
1st argument given is an Integer x.
2nd argument given is an Integer y.
3rd argument given is an Integer N, number of circles.
4th argument given is an Integer R, radius of each circle.
5th argument given is an Array A of size N, where A[i] = x cordinate of ith circle
6th argument given is an Array B of size N, where B[i] = y cordinate of ith circle

```

**Output Format**

```
Return YES or NO depending on weather it is possible to reach cell (x,y) or not starting from (0,0).

```

**Constraints**

```
0 <= x, y, R <= 100
1 <= N <= 1000
Center of each circle would lie within the grid

```

**For Example**

```
Input:
    x = 2
    y = 3
    N = 1
    R = 1
    A = [2]
    B = [3]
Output:
    NO

Explanation:
    There is NO valid path in this case

```

```cpp
string Solution::solve(int A, int B, int C, int D, vector<int> &E, vector<int> &F) {
    
    int x[8]={1,1,1,0,0,-1,-1,-1}; // for all 8 directions
    int y[8]={0,1,-1,1,-1,0,1,-1};
    
    vector<vector<bool>> mat(A+1, vector<bool>(B+1));
    
    // check each point is inside of any circle or not
    for(int i = 0; i<=A; i++){
        for(int j = 0; j<=B; j++){
            bool flag = false;
            for(int k = 0; k<E.size(); k++){
                if((E[k] - i)*(E[k] - i) + (F[k] - j)*(F[k] - j) <= D*D){
                    flag = true;
                }
            }
            mat[i][j] = flag;
        }
    }
    
    // if starting index is insider of any circle
    if(mat[0][0] == true) return "NO";
    queue<pair<int, int>> q;
    q.push({0,0});
    
    // using the same bool matrix to make visited
    mat[0][0] = true;
    
    while(!q.empty()){
        pair<int, int> temp = q.front();
        q.pop();
        
        // reach our destination
        
        if(temp.first == A and temp.second  == B) return "YES";
        
        // go in all 8 possible directions
        
        for(int i = 0; i<8; i++){
            int newx = x[i] + temp.first;
            int newy = y[i] + temp.second;
            
            // if inside the boundary and not insider of any circle
            if(newx>=0 and newy>=0 and newx<=A and newy <= B and mat[newx][newy] == false){
                q.push({newx, newy});
                
                // visit the co-ordinates
                mat[newx][newy] = true;
            }
        } 
    }
    return "NO";

}
```