# Find the number of islands | Practice | GeeksforGeeks

Created: August 11, 2022 5:00 PM
Tags: Graphs
URL: https://practice.geeksforgeeks.org/problems/find-the-number-of-islands/1

Given a grid of size n*m (n is the number of rows and m is the number of columns in the grid) consisting of '0's (Water) and '1's(Land). Find the number of islands.

**Note:** An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically or diagonally i.e., in all 8 directions.

**Example 1:**

```
Input:
grid = {{0,1},{1,0},{1,1},{1,0}}
Output:
1
Explanation:
The grid is-
0 1
1 0
1 1
1 0
All lands are connected.

```

**Example 2:**

```
Input:
grid = {{0,1,1,1,0,0,0},{0,0,1,1,0,1,0}}
Output:
2
Expanation:
The grid is-
0 1 1 1 0 0 0
0 0 1 1 0 1 0
There are two islands :- one is colored in blue
and other in orange.

```

**Your Task:**
 You don't need to read or print anything. Your task is to complete the function **numIslands()** which takes the grid as an input parameter and returns the total number of islands.

**Expected Time Complexity:** O(n*m)**Expected Space Complexity:** O(n*m)

**Constraints:**
 1 ≤ n, m ≤ 500

```cpp
//{ Driver Code Starts
#include <bits/stdc++.h>
using namespace std;

// } Driver Code Ends
class Solution {
  public:
    // Function to find the number of islands.
    int numIslands(vector<vector<char>>& A) {
        // Code here
        int n = A.size();
        int m = A[0].size();
        int dx[] = {1,1,1,-1,-1,-1,0,0};
        int dy[] = {1,0,-1,1,0,-1,1,-1};
    
    
        queue<pair<int, int>> q;
        int ans = 0;
        
        for(int i = 0; i<n; i++){
            for(int j = 0; j<m; j++){
                if(A[i][j] == '1'){
                    ans++;
                    q.push({i, j});
                    A[i][j] = '0';
                    while(!q.empty()){
                        int x = q.front().first;
                        int y = q.front().second;
                        
                        q.pop();
                        for(int k = 0; k<8; k++){
                            int nx = x + dx[k];
                            int ny = y + dy[k];
                            
                            if(nx>=0 and ny>=0 and nx<n and ny<m  and A[nx][ny] == '1'){
                                A[nx][ny] = '0';
                                q.push({nx, ny});
                            }
                        }
                        
                    }
                }
            }
        }
        
        return ans;
    }
};
```