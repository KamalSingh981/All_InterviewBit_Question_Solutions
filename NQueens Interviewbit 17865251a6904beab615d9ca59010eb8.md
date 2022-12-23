# NQueens | Interviewbit

Created: July 2, 2022 1:16 AM
Tags: Backtracking, Recursion
URL: https://www.interviewbit.com/problems/nqueens/

The n-queens puzzle is the problem of placing n queens on an n×n chessboard such that no two queens attack each other.

![NQueens%20Interviewbit%2017865251a6904beab615d9ca59010eb8/yaxpgda.png](NQueens%20Interviewbit%2017865251a6904beab615d9ca59010eb8/yaxpgda.png)

Given an integer n, return all distinct solutions to the n-queens puzzle.

Each solution contains a distinct board configuration of the n-queens’ placement, where `'Q'` and `'.'` both indicate a queen and an empty space respectively.

For example,
 There exist two distinct solutions to the 4-queens puzzle:

```cpp
bool isSafe(int A, int i, int j, int board[][100]){
    
    // For same column
    for(int row = 0; row < i; row++){
        if(board[row][j] == 1){
            return false;
        }
    }
    
    // For diagonals
    int x = i;
    int y = j;
    while(x >=0 and y>=0){
        if(board[x][y] == 1){
            return false;
        }
        
        x--;
        y--;
    }
    
    x = i;
    y = j;
    
    while(x>=0 and y>=0){
        if(board[x][y] == 1){
            return false;
        }
        
        x--;
        y++;
    }
    
    return true;
    
    
}

vector<vector<string>> ans;

bool NQueen(int A, int i, int board[][100]){
    if(i == A){
        vector<string> temp;
        for(int k = 0; k<A; k++){
            string m = "";
            for(int l  = 0; l<A; l++){
                if(board[k][l] == 1){
                    m += "Q";
                }
                else{
                    m += ".";
                }
            }
            temp.push_back(m);
        }
        ans.push_back(temp);
        return false; 
    }
    
    for(int k = 0; k<A; k++){
        if(isSafe(A, i, k, board)){
            board[i][k] = 1;
        
        
        bool nextQueen = NQueen(A, i+1, board);
        if(nextQueen){
            return true;
        }
        
        board[i][k] = 0;
        }
    }
    return false;
}

vector<vector<string> > Solution::solveNQueens(int A) {
    ans.clear();
    int board[100][100] = {0};
    NQueen(A, 0, board);
    return ans;
}
```