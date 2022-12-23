# Google Question- The Reaching point

Created: November 8, 2022 1:22 AM
Tags: BFS, Graphs

```cpp
#include <bits/stdc++.h>
#include <iostream>

using namespace std;

void bfs(vector<vector<int>> &grid, int i, int j, int x, int y) {
    int n = grid.size();
    int m = grid[0].size();

    queue<pair<pair<int, int>, int>> q;
    q.push({{i, j}, 0});

    set<pair<int, int>> s;
    s.insert({i, j});

    bool ans = true;
  int dx[4] = {0,0,-1,1};
  int dy[4] = {1,-1,0,0};

    while(!q.empty()){
        int x1 = q.front().first.first;
        int x2 = q.front().first.second;
        int dis = q.front().second;
        q.pop();

        if(x1 == x and x2 == y){
            cout << "Yes" << endl;
            break;
        }
        if(grid[x1-1][x2-1]%grid[x-1][y-1] == 0 and dis<=3){
            cout << "Yes";
            ans = false;
            break;
        }

        if(dis<4) {
            for (int i = 0; i < 4; i++) {
                int newx = x1 + dx[i];
                int newy = x2 + dy[i];

                if(x1 < n and x2 < m and x1 >=0 and x2 >= 0 and s.find({newx, newy}) == s.end()){
                    s.insert({newx, newy});
                    q.push({{newx, newy}, dis + 1});
                }
            }
        }
    }
    if(ans) {
        cout << "No";
    }
}

int main(){

    vector<vector<int>> grid = {{7,3,25,9,7,50}, {3,11,10,12,33,6}, { 5,20,1,8,15,36}};
    int n = grid.size();
    int m = grid[0].size();
    vector<vector<int>> queries = {{3, 1, 1, 5}};
    bfs(grid, queries[0][0], queries[0][1], queries[0][2], queries[0][3]);

}
```