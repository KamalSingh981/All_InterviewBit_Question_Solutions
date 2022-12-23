# Set Matrix Zeros | Interviewbit

Created: May 9, 2022 3:32 PM
URL: https://www.interviewbit.com/problems/set-matrix-zeros/

**Problem Description**

Given a matrix, **A** of size **M** x **N** of **0s** and **1s**. If an element is **0**, set its entire row and column to **0**.

**Note**: This will be evaluated on the extra memory used. Try to minimize the space and time complexity.

**Input Format:**

```
The first and the only argument of input contains a 2-d integer matrix, A, of size M x N.

```

**Output Format:**

```
Return a 2-d matrix that satisfies the given conditions.

```

**Constraints:**

```
1 <= N, M <= 1000
0 <= A[i][j] <= 1

```

**Examples:**

```
Input 1:
    [   [1, 0, 1],
        [1, 1, 1],
        [1, 1, 1]   ]

Output 1:
    [   [0, 0, 0],
        [1, 0, 1],
        [1, 0, 1]   ]Input 2:
    [   [1, 0, 1],
        [1, 1, 1],
        [1, 0, 1]   ]Output 2:
    [   [0, 0, 0],
        [1, 0, 1],
        [0, 0, 0]   ]

```

```cpp
#include <utility>

void Solution::setZeroes(vector<vector<int> > &A) {
    int col[A[0].size()] = {0};
    int row[A.size()] = {0};
    int m = A.size();
    int n = A[0].size();
    for(int i=0; i<m; i++){
        for (int j=0; j<n; j++){
            if(A[i][j]==0){
                row[i] = 1;
                col[j] = 1; 
            }
        }
    }
    for(int i=0; i<m; i++){
        for(int j=0; j<n; j++){
            if(col[j]==1 || row[i]==1){
            A[i][j] = 0;
        }
    }   
}
}
```