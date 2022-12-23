# Kth Manhattan Distance Neighbourhood | Interviewbit

Created: August 9, 2022 3:16 AM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/kth-manhattan-distance-neighbourhood/

Given a matrix M of size nxm and an integer K, find the maximum element in the K manhattan distance neighbourhood for all elements in nxm matrix. 
 In other words, for every element M[i][j] find the maximum element M[p][q] such that `abs(i-p)+abs(j-q) <= K`.

`Note: Expected time complexity is O(N*N*K)`

**Constraints:**

```
1 <= n <= 300
1 <= m <= 300
1 <= K <= 300
0 <= M[i][j] <= 1000

```

**Example:**

```cpp
int x[4] = {1,-1,0,0};
int y[4] = {0,0,-1,1};

int tellTheFuckingAnswer(vector<vector<int>> &B, int A, vector<vector<vector<int>>> &dp, int i, int j){
    if(i<0 || j<0 || i>=B.size() || j>=B[0].size()){
        return 0;
    }
    
    if(A==0) return B[i][j];
    
    
    if(dp[i][j][A] != -1) return dp[i][j][A];
    
    int ans = B[i][j];
    for(int k = 0; k<4; k++){
        ans = max(ans, tellTheFuckingAnswer(B, A -1, dp, i + x[k], j + y[k]));
    }
    
    return dp[i][j][A] = ans;
}

vector<vector<int> > Solution::solve(int A, vector<vector<int> > &B) {
    
    int n = B.size();
    int m = B[0].size();
    
    vector<vector<int>> ans(n, vector<int>(m, 0));
    vector<vector<vector<int>>> dp(n, vector<vector<int>>(m, vector<int>(A + 1, -1)));
    
    for(int i = 0; i<n; i++){
        for(int j = 0; j<m; j++){
            ans[i][j] = tellTheFuckingAnswer(B, A, dp, i, j);
        }
    }
    
    return ans;
}
```