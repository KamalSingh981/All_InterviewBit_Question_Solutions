# Matrix Search | Interviewbit

Created: May 25, 2022 12:04 AM
Tags: Binary Search
URL: https://www.interviewbit.com/problems/matrix-search/

Given a matrix of integers **A** of size **N x M** and an integer **B**.

Write an efficient algorithm that searches for integar **B** in matrix **A**.

This matrix **A** has the following properties:

> 
> 
> 1. Integers in each row are sorted from left to right.
> 2. The **first integer** of each row is greater than or equal to the **last integer** of the previous row.

Return **1** if **B** is present in **A**, else return **0**.

**Note:** Rows are numbered from top to bottom and columns are numbered from left to right.

**Input Format**

```
The first argument given is the integer matrix A.
The second argument given is the integer B.

```

**Output Format**

```
Return 1 if B is present in A, else return 0.

```

**Constraints**

```
1 <= N, M <= 1000
1 <= A[i][j], B <= 10^6

```

**For Example**

```
Input 1:
    A =
    [ [1,   3,  5,  7],
      [10, 11, 16, 20],
      [23, 30, 34, 50]  ]
    B = 3
Output 1:
    1

Input 2:
    A = [   [5, 17, 100, 111]
            [119, 120,  127,   131]    ]
    B = 3
Output 2:
    0

```

My Code

```cpp
int Solution::searchMatrix(vector<vector<int> > &A, int B) {
    int l = 0;
    int r= A.size()*A[0].size();
    vector<int> a;
    for(int i = 0; i<A.size(); i++){
        for(int j=0; j<A[0].size(); j++){
            a.push_back(A[i][j]);
        }
    }

    int mid;
    while(l<=r){
        mid = l + (r-l)/2;
        if(a[mid] == B){
            return 1;
        }
        else if(a[mid]>B){
            r = mid -1;
        }
        else{
            l = mid +1;
        }
    }
    return 0;
```

Interview Bit code

```cpp
int Solution::searchMatrix(vector<vector<int> > &A, int B) {
    int N=A.size();
    int M=A[0].size();
    int start=0, end=N*M-1;
    while(start<=end){
        int mid=start+(end-start)/2;
        int x=mid/M;
        int y=mid%M;
        if(A[x][y]==B) return 1;
        if(B<A[x][y]) end=mid-1;
        else start=mid+1;
    }
    return 0;
}
```