# Maximum Sum Square SubMatrix | Interviewbit

Created: May 15, 2022 1:22 PM
URL: https://www.interviewbit.com/problems/maximum-sum-square-submatrix/

**Problem Description**

Given a 2D integer matrix **A** of size `N x N` find a `B x B` submatrix where B<= N and B>= 1, such that **sum of all the elements in submatrix is maximum**.

**Problem Constraints**

1 <= N <= 103.

1 <= B <= N

- 10 <= A[i][j] <= 10.
    
    2
    
    2
    

**Input Format**

First arguement is an 2D integer matrix **A**.

Second argument is an integer **B**.

**Output Format**

Return a single integer denoting the maximum sum of submatrix of size `B x B`.

**Example Input**

Input 1:

```
 A = [
        [1, 1, 1, 1, 1]
        [2, 2, 2, 2, 2]
        [3, 8, 6, 7, 3]
        [4, 4, 4, 4, 4]
        [5, 5, 5, 5, 5]
     ]
 B = 3

```

Input 2:

```
 A = [
        [2, 2]
        [2, 2]
    ]
 B = 2

```

**Example Output**

**Example Explanation**

Explanation 1:

```
    Maximum sum 3 x 3 matrix is
    8 6 7
    4 4 4
    5 5 5
    Sum = 48

```

Explanation 2:

```
 Maximum sum 2 x 2 matrix is
  2 2
  2 2
  Sum = 8

```

```cpp
int printSumTricky(vector<vector<int>> mat, int k, int n)
{
    int stripSum[n][n];
 
    for (int j = 0; j < n; j++) {
    
        int sum = 0;
        for (int i = 0; i < k; i++)
            sum += mat[i][j];
        stripSum[0][j] = sum;
 
        for (int i = 1; i < n - k + 1; i++) {
            sum += (mat[i + k - 1][j] - mat[i - 1][j]);
            stripSum[i][j] = sum;
        }
    }
     int maxi = INT_MIN;
    for (int i = 0; i < n - k + 1; i++) {
        int sum = 0;
        for (int j = 0; j < k; j++)
            sum += stripSum[i][j];
            maxi = max(maxi, sum);
        for (int j = 1; j < n - k + 1; j++) {
            sum += (stripSum[i][j + k - 1]
                    - stripSum[i][j - 1]);
            maxi = max(maxi, sum);
        }
    }
    return maxi;
}
int Solution::solve(vector<vector<int> > &A, int B) {
    int n = A.size();
    return printSumTricky(A, B, n);
}
```