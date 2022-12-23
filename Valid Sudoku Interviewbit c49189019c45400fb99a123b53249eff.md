# Valid Sudoku | Interviewbit

Created: July 15, 2022 6:36 PM
Tags: Hashing
URL: https://www.interviewbit.com/problems/valid-sudoku/

Determine if a Sudoku is valid, according to: http://sudoku.com.au/TheRules.aspx

The Sudoku board could be partially filled, where empty cells are filled with the character ‘.’.

![Valid%20Sudoku%20Interviewbit%20c49189019c45400fb99a123b53249eff/250px-Sudoku-by-L2G-20050714.svg.png](Valid%20Sudoku%20Interviewbit%20c49189019c45400fb99a123b53249eff/250px-Sudoku-by-L2G-20050714.svg.png)

The input corresponding to the above configuration :

A partially filled sudoku which is valid.

> 
> 
> 
> **Note:**
> 
> - A valid Sudoku board (partially filled) is not necessarily solvable. Only the filled cells need to be validated.

**Return `0 / 1` ( 0 for false, 1 for true ) for this problem**

```cpp
int Solution::isValidSudoku(const vector<string> &A) {
    for(int i =0; i<9; i++){
        unordered_map<char, int> rm;
        unordered_map<char, int> cm;
        for(int j =0; j<9; j++){
            char rc = A[i][j];
            char cc = A[j][i];
            if(rc != '.'){
                if(rm.find(rc) != rm.end()){
                    return 0;
                }
                else{
                    rm[rc]++;
                }
            } 
            if(cc != '.'){
                if(cm.find(cc) != cm.end()){
                    return 0;
                }
                else{
                    cm[cc]++;
                }
            }           
        }
    }
    unordered_map<string, int> bx;
    for(int i = 0; i<A.size(); i++){
        for(int j = 0; j<A.size(); j++){
            char c = A[i][j];
            if(c != '.'){
                string d = "";
                d.push_back(i/3);
                d.push_back((j/3));
                d.push_back((c));
                if(bx.find(d) != bx.end()){
                    return 0;
                }
                else{
                    bx[d]++;
                }
            }
        }
    }
    
    return 1;
```