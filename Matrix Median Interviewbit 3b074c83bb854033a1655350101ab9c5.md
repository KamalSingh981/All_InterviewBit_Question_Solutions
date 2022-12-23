# Matrix Median | Interviewbit

Created: June 18, 2022 2:15 PM
Tags: Binary Search
URL: https://www.interviewbit.com/problems/matrix-median/

Given a matrix of integers **A** of size **N x M** in which each row is sorted.

Find an return the overall median of the matrix **A**.

**Note:** No extra memory is allowed.

**Note:** Rows are numbered from top to bottom and columns are numbered from left to right.

**Input Format**

```
The first and only argument given is the integer matrix A.

```

**Output Format**

```
Return the overall median of the matrix A.

```

**Constraints**

```
1 <= N, M <= 10^5
1 <= N*M  <= 10^6
1 <= A[i] <= 10^9
N*M is odd

```

**For Example**

```
Input 1:
    A = [   [1, 3, 5],
            [2, 6, 9],
            [3, 6, 9]   ]
Output 1:
    5
Explanation 1:
    A = [1, 2, 3, 3, 5, 6, 6, 9, 9]
    Median is 5. So, we return 5.

Input 2:
    A = [   [5, 17, 100]    ]
Output 2:
    17 ``` Matrix=

```

```

```cpp
int Solution::findMedian(vector<vector<int> > &A) {
    int r = A.size();
    int c = A[0].size();
    int maxi = INT_MIN;
    int mini = INT_MAX;
    for(int i=0; i<r; i++){
        mini = min(mini, A[i][0]);
        maxi = max(maxi, A[i][c-1]);
    }
    
    int desired = (r*c + 1)/2 ;
    while(mini < maxi){
        int mid = (mini + maxi)/2;
        int place = 0;
        for(int i =0; i<r; i++){
            place += upper_bound(A[i].begin(), A[i].end(), mid) - A[i].begin();
        }
        if(place<desired){
            mini = mid +1;
        }
        else{
            maxi = mid;
        }
    }
    return mini;
}
```