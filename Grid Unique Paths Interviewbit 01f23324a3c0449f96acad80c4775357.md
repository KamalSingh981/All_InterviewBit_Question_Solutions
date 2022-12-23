# Grid Unique Paths | Interviewbit

Created: May 18, 2022 7:50 PM
URL: https://www.interviewbit.com/problems/grid-unique-paths/

```cpp

```

A robot is located at the top-left corner of an **A x B grid** (marked ‘Start’ in the diagram below).

![Grid%20Unique%20Paths%20Interviewbit%2001f23324a3c0449f96acad80c4775357/3eaivQ5.png](Grid%20Unique%20Paths%20Interviewbit%2001f23324a3c0449f96acad80c4775357/3eaivQ5.png)

The robot can only move either down or right at any point in time. The robot is trying to reach the bottom-right corner of the grid (marked ‘Finish’ in the diagram below).

How many possible unique paths are there?

*Note: A and B will be such that the resulting answer fits in a 32 bit signed integer.*

**Example :**

```cpp
int Solution::uniquePaths(int A, int B) {
    int arr[A][B];
    for(int i=0; i<B;i++){
        arr[0][i] = 1;
    }
    for(int i=0; i<A; i++){
        arr[i][0] = 1;
    }
    for(int i = 1; i<A; i++){
        for(int j=1; j<B; j++){
            arr[i][j] = arr[i-1][j] + arr[i][j-1];
        }
    }
    return arr[A-1][B-1];
}
```