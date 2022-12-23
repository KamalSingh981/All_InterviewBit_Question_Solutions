# Knight On Chess Board | Interviewbit

Created: July 26, 2022 6:50 PM
Tags: BFS, Graphs
URL: https://www.interviewbit.com/problems/knight-on-chess-board/

Given any source point, **(C, D)** and destination point, **(E, F)** on a chess board, we need to find whether Knight can move to the destination or not.

![Knight%20On%20Chess%20Board%20Interviewbit%20e8a237dac9c3400a94d2d4d76e3b3a4d/lmKL4AU.jpg](Knight%20On%20Chess%20Board%20Interviewbit%20e8a237dac9c3400a94d2d4d76e3b3a4d/lmKL4AU.jpg)

The above figure details the movements for a knight ( 8 possibilities ).

If yes, then what would be the **minimum** number of steps for the knight to move to the said point.
 If knight can not move from the source point to the destination point, then return **-1**.

**Note:** A knight cannot go out of the board.

**Input Format:**

```
The first argument of input contains an integer A.
The second argument of input contains an integer B.
    => The chessboard is of size A x B.
The third argument of input contains an integer C.
The fourth argument of input contains an integer D.
    => The Knight is initially at position (C, D).
The fifth argument of input contains an integer E.
The sixth argument of input contains an integer F.
    => The Knight wants to reach position (E, F).

```

**Output Format:**

```
If it is possible to reach the destination point, return the minimum number of moves.
Else return -1.

```

**Constraints:**

```
1 <= A, B <= 500

```

**Example**

```
Input 1:
    A = 8
    B = 8
    C = 1
    D = 1
    E = 8
    F = 8

Output 1:
    6

Explanation 1:
    The size of the chessboard is 8x8, the knight is initially at (1, 1) and the knight wants to reach position (8, 8).
    The minimum number of moves required for this is 6.

```

```cpp
int Solution::knight(int A, int B, int C, int D, int E, int F) {
    bool visited[A][B];
    int dist[A][B];
    for(int i = 0; i<A; i++){
        for(int j =0; j<B; j++){
            visited[i][j] = false;
            dist[i][j] = 0;
        }
    }

    queue<pair<int, int>> q;

    int knightx[] = {1,1,-1,-1,2,2,-2,-2};
    int knighty[] = {2,-2,2,-2,1,-1,1,-1};

    q.push({C-1, D-1});
    visited[C-1][D-1] = true;
    while(!q.empty()){
        pair<int , int> temp = q.front();
        q.pop();
        if(temp == make_pair(E-1,F-1)){
            return dist[temp.first][temp.second];
        }
        
        for(int i = 0; i<8; i++){
            int x = temp.first - knightx[i], y = temp.second - knighty[i];
            if(x>=0 and x<A and y>=0 and y<B and visited[x][y] == false){
                q.push({x,y});
                visited[x][y] = true;
                dist[x][y] = dist[temp.first][temp.second] + 1;
            }
        } 
    }
    return -1;
}
```