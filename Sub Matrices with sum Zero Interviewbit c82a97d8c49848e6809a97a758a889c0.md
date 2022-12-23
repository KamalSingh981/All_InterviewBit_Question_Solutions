# Sub Matrices with sum Zero | Interviewbit

Created: August 1, 2022 2:12 AM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/sub-matrices-with-sum-zero/

Given a 2D matrix, find the number non-empty sub matrices, such that the sum of the elements inside the sub matrix is equal to 0. (note: elements might be negative).

**Example:**

**Input**

```
-8 5  7
3  7 -8
5 -8  9

```

**Output**
 2

**Explanation-8** 5 7**3** 7 -8**5** -8 9

- 8 5 7 3 **7 -8** 5 **8 9**

```cpp
int subarrayTarget(vector<int> &a){
    int n = a.size();
    unordered_map<int, int> m;
    
    int ans = 0;
    m[0] = 1;
    long long sum = 0;
    for(int i = 0; i<n; i++){
        sum += a[i];
        if(m.find(sum) != m.end()){
            ans += m[sum];
        }
        m[sum]++;
    }
    return ans;
    
}

int Solution::solve(vector<vector<int> > &A) {
    
    int rows = A.size();
    if(rows==0) return 0;
    int columns = A[0].size();
    
    long long ans = 0; // stores the ans
    
    for(int startcol = 0; startcol<columns; startcol++){
        vector<int> submatrixArray(rows, 0);
        for(int endcol = startcol; endcol <columns; endcol++){
            for(int row = 0; row<rows; row++){
                submatrixArray[row] += A[row][endcol];
            }
            ans +=subarrayTarget(submatrixArray);
        }
    }

    return ans;
}
```