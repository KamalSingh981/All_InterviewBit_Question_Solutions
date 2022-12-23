# Sudoku | Interviewbit

Created: July 12, 2022 8:02 PM
Tags: Backtracking, Recursion
URL: https://www.interviewbit.com/problems/sudoku/

Write a program to solve a Sudoku puzzle by filling the empty cells.
 Empty cells are indicated by the character `'.'` 
 You may assume that there will be only one unique solution.

![Sudoku%20Interviewbit%207b07823b78b34ec1a703cae9c6c6d824/250px-Sudoku-by-L2G-20050714.svg.png](Sudoku%20Interviewbit%207b07823b78b34ec1a703cae9c6c6d824/250px-Sudoku-by-L2G-20050714.svg.png)

A sudoku puzzle,

![Sudoku%20Interviewbit%207b07823b78b34ec1a703cae9c6c6d824/250px-Sudoku-by-L2G-20050714_solution.svg.png](Sudoku%20Interviewbit%207b07823b78b34ec1a703cae9c6c6d824/250px-Sudoku-by-L2G-20050714_solution.svg.png)

and its solution numbers marked in red.

**Note**: You must update the input argument A (partially completed grid of Sudoku) to submit your solved Sudoko grid.

**Example :**

For the above given diagrams, the corresponding input to your program will be

```
[[53..7....], [6..195...], [.98....6.], [8...6...3], [4..8.3..1], [7...2...6], [.6....28.], [...419..5], [....8..79]]

```

and we would expect your program to modify the above array of array of characters to

```
[[534678912], [672195348], [198342567], [859761423], [426853791], [713924856], [961537284], [287419635], [345286179]]

```

```cpp
bool canPlace(vector<vector<char>> A, int i, int j, char x, int n){
    // For Column and row condition
    for(int k = 0; k<n;k++){
        if(A[k][j] == x or A[i][k] == x){
            return false;
        }
    }   
    // Checking for Cube condition.    
    int sq = sqrt(n);
    int cx = (i/sq)*sq;
    int cy = (j/sq)*sq;
    for(int t = cx; t<cx + sq; t++){
        for(int u = cy; u<cy+sq; u++){
            if(A[t][u] == x){
                return false;
            }
        }
    }
       
    return true;
}

bool Sudoku(vector<vector<char>> &A, int i, int j, int n){
    if(i == n){
        return true;
    }
    if(j == n){
        return Sudoku(A, i+1, 0, n);
    }
    
    if(A[i][j] != '.'){
        return Sudoku(A, i, j + 1, n);
    }
    for(int x = 1; x <= n; x++){
        if(canPlace(A, i, j, x + '0', n)){
            A[i][j] = x + '0';
            
            bool cansolve = Sudoku(A, i, j, n);
            if(cansolve == true){
                return true;
            }
        }
        
    }
    
    A[i][j] = '.';
    return false;
    
}

void Solution::solveSudoku(vector<vector<char> > &A) {
    // Do not write main() function.
    // Do not read input, instead use the arguments to the function.
    // Do not print the output, instead return values as specified
    // Still have a doubt. Checkout www.interviewbit.com/pages/sample_codes/ for more details
```