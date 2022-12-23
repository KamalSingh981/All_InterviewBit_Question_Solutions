# Maximum Size Square Sub-matrix | Interviewbit

Created: August 2, 2022 3:44 PM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/maximum-size-square-sub-matrix/

**Problem Description**

Given a 2D binary matrix **A** of size  `N x M`  find the area of **maximum size square sub-matrix** with all **1's**.

**Problem Constraints**

1 <= N, M <= 103

A[i][j] = 1 or A[i][j] = 0

**Input Format**

First argument is an 2D matrix **A** of size `N x M`.

**Output Format**

Output the area of **maximum size square sub-matrix** in **A** with all **1's**.

**Example Input**

Input 1:

```
 A = [

        [0, 1, 1, 0, 1],

        [1, 1, 0, 1, 0],

        [0, 1, 1, 1, 0],

        [1, 1, 1, 1, 0],

        [1, 1, 1, 1, 1],

        [0, 0, 0, 0, 0]
     ]

```

Input 2:

```
 A = [

       [1, 1],
       [1, 1]
     ]

```

**Example Output**

**Example Explanation**

Explanation 1:

```
  Consider the below binary matrix.

 The area of the square is 3 * 3 = 9

```

Explanation 2:

```
 The given matrix is the largest size square possible so area will be 2 * 2 = 4

```

```cpp
int Solution::solve(vector<vector<int> > &A) {
    int n = A.size();
    int m = A[0].size();
    
    int ans = 0;
        
    for(int  i = 0; i<n; i++){
        for(int j = 0; j<m; j++){
            if(A[i][j] == 1){
                if(i and j){
                    A[i][j] = min(min(A[i-1][j], A[i][j-1]), A[i-1][j-1]) + 1;
                }
                ans = max(ans, A[i][j]);
            }
        }
    }
    return ans*ans;   
}
```