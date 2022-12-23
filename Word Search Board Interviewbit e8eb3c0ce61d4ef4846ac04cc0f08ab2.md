# Word Search Board | Interviewbit

Created: July 29, 2022 3:53 PM
Tags: DFS, Graphs
URL: https://www.interviewbit.com/problems/word-search-board/

Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where `"adjacent"` cells are those horizontally or vertically neighboring. The cell itself does not count as an adjacent cell. 
 The same letter cell may be used more than once.

**Example :**

Given board =

```
[
  ["ABCE"],
  ["SFCS"],
  ["ADEE"]
]

```

```
word = "ABCCED", -> returns 1,
word = "SEE", -> returns 1,
word = "ABCB", -> returns 1,
word = "ABFSAB" -> returns 1
word = "ABCD" -> returns 0

```

Note that 1 corresponds to true, and 0 corresponds to false.

```cpp
int dx[] = {0,0,-1,1};
int dy[] = {1,-1,0,0};

bool dfs(int i , int j, int index, vector<string> &A, string &B, int &r, int &c){
    if(index == B.length()-1){
        return true;
    }
    
    index++;
    
    for(int t =0; t<4; t++){
        int x = i + dx[t];
        int y = j + dy[t];
        if(x>=0 and x<r and y>=0 and y<c and A[x][y] == B[index]){
            if(dfs(x, y, index, A, B, r, c)) 
                return true;
        }
    }
    // if no matach is found
    return false;
}

int Solution::exist(vector<string> &A, string B) {
    
    int r = A.size();
    int c = A[0].size();
    

    for(int i =0; i<r; i++){
        for(int  j = 0; j<c; j++){
            if(A[i][j] == B[0]){
                if(dfs(i, j, 0, A, B, r, c)){
                    return 1;
                }
            }
        }
    }      
    return 0;
}
```