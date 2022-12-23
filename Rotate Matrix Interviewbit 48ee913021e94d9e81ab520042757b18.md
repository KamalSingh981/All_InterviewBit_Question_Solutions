# Rotate Matrix | Interviewbit

Created: May 15, 2022 12:22 AM
URL: https://www.interviewbit.com/problems/rotate-matrix/

You are given an n x n 2D matrix representing an image.

Rotate the image by 90 degrees (clockwise).

You need to do this in place.

Note that if you end up using an additional array, you will only receive partial score.

**Example:**

If the array is

```
[
    [1, 2],
    [3, 4]
]

```

Then the rotated array becomes:

```cpp
void Solution::rotate(vector<vector<int> > &A) {
    int n = A.size();
    for(int i = 0; i<n; i++){
        for(int j =i; j<n; j++){
            int temp = A[i][j];
            A[i][j] = A[j][i];
            A[j][i] = temp;
        }
    }

    for(int i = 0; i <n; i++){
        for(int j=0; j<n/2; j++){
            int temp = A[i][j];
            A[i][j] = A[i][n-1 -j];
            A[i][n-1-j]= temp;
        }
    }

}
```