# Largest area of rectangle with permutations | Interviewbit

Created: August 9, 2022 10:19 PM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/largest-area-of-rectangle-with-permutations/

**Problem Description**

Given a binary grid **A** of size `N x M` consisting of 0's and 1's, find the **area of the largest rectangle** inside the grid such that all the cells inside the chosen rectangle should have 1 in them.

You are allowed to permutate the columns matrix i.e. you can arrange each of the column in any order in the final grid.

Please follow the sample input and explanation for more clarity.

**Input Format**

First and only argument is an 2D binary array **A**.

**Output Format**

Return a single integer denoting the **area of the largest rectangle** inside the grid such that all the cells inside the chosen rectangle should have 1 in them.

**Example Input**

Input 1:

```
 A = [  [1, 0, 1]
        [0, 1 ,0]
        [1, 0, 0]
    ]

```

**Example Output**

**Example Explanation**

Explanation 1:

```
    1 0 1
    0 1 0
    1 0 0

At present we can see that max rectangle satisfying the criteria mentioned in the problem
 is of 1 * 1 = 1 area i.e either of the 4 cells which contain 1 in it.Now since we are allowed to permutate the columns of the given matrix, we can take column 1
 and column 3 and make them neighbours. One of the possible configuration of the grid can be:
 1 1 0
 0 0 1
 1 0 0Now In this grid, first column is column 1, second column is column 3 and third column
 is column 2 from the original given grid.Now, we can see that if we calculate the max area rectangle, we get max area as 1 * 2 = 2
 which is bigger than the earlier case. Hence 2 will be the answer in this case.

```

```cpp
int count_sort(vector<int>& v,int n){
    vector<int> count(n+1,0);
    for(auto x: v){
        count[x]+=1;
    }
    int result = 0;
    int width = 0;
    for(int i = n;i>=0;i--){
        if(count[i] ==0 ) continue;
        width += count[i];
        result = max(result,width * i);
    }

    return result;
}
int Solution::solve(vector<vector<int> > &A) {
    int n = A.size();
    if(n==0)return 0;
    int m = A[0].size();
    vector<vector<int>> count(n,vector<int>(m,0));

    for(int i = 0;i<n;i++){
        for(int j = 0;j<m;j++){
            if(i==0){
                count[i][j] = A[i][j];
            }
            else{
                count[i][j] = A[i][j] * (count[i-1][j] + 1);
            }
        }
    }
    int result = 0;
    for(int i = 0;i<n;i++){
        // for each row we need to sort the row using count sort;
        result = max(result, count_sort(count[i],n));
    }

    return result;
}
```