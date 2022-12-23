# Spiral Order Matrix II | Interviewbit

Created: May 9, 2022 1:38 AM
URL: https://www.interviewbit.com/problems/spiral-order-matrix-ii/

Given an integer **A**, generate a square matrix filled with elements from **1** to **A2** in **spiral order**.

**Input Format:**

```
The first and the only argument contains an integer, A.

```

**Output Format:**

```
Return a 2-d matrix of size A x A satisfying the spiral order.

```

**Constraints:**

**Examples:**

```
Input 1:
    A = 3

Output 1:
    [   [ 1, 2, 3 ],
        [ 8, 9, 4 ],
        [ 7, 6, 5 ]   ]

Input 2:
    4

Output 2:
    [   [1, 2, 3, 4],
        [12, 13, 14, 5],
        [11, 16, 15, 6],
        [10, 9, 8, 7]   ]

```

```cpp
vector<vector<int> > Solution::generateMatrix(int A) {
    int r = 0;
    int s = A-1;
    int t = A-1;
    int u = 0;
    int range = A*A;
    int j= 1;
    int d = 0; // direction
    vector<vector<int>> ans( A , vector<int> (A));
    while(j<=range){
        if(d ==0){
            for(int i=u; i<=t; i++){
                ans[r][i] = j;
                j+=1;
            }
            d = 1;
            r+=1;
        }
        else if(d ==1){
            for(int i=r; i<=s; i++){
                ans[i][t] = j;
                j+=1;
            }
            d = 2;
            t-=1;
        }
        else if(d == 2){
            for(int i=t; i>=u; i--){
                ans[s][i] = j;
                j+=1;
            }
            d = 3;
            s-=1;
        }
        else if(d ==3){
            for(int i=s; i>=r; i--){
                ans[i][u] = j;
                j+=1;
            }
            d = 0;
        u+=1;
        }     
    }
    return ans;
}
```