# Dungeon Princess | Interviewbit

Created: August 2, 2022 9:56 PM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/dungeon-princess/

The demons had captured the princess **(P)** and imprisoned her in the bottom-right corner of a dungeon. The dungeon consists of `M x N` rooms laid out in a 2D grid. Our valiant knight **(K)** was initially positioned in the top-left room and must fight his way through the dungeon to rescue the princess.

The knight has an initial health point represented by a positive integer. If at any point his health point drops to 0 or below, he dies immediately.

Some of the rooms are guarded by demons, so the knight loses health (negative integers) upon entering these rooms; other rooms are either empty (0’s) or contain magic orbs that increase the knight’s health (positive integers).

In order to reach the princess as quickly as possible, the knight decides to move only rightward or downward in each step.

**Write a function to determine the knight’s minimum initial health so that he is able to rescue the princess.**

For example, given the dungeon below, the initial health of the knight must be at least 7 if he follows the optimal path

`RIGHT-> RIGHT -> DOWN -> DOWN`.

![Dungeon%20Princess%20Interviewbit%20707fe8dee2124d00ba6add25a6ac3f41/5a6Neu4.png](Dungeon%20Princess%20Interviewbit%20707fe8dee2124d00ba6add25a6ac3f41/5a6Neu4.png)

**Input arguments to function:**
 Your function will get an M*N matrix (2-D array) as input which represents the 2D grid as described in the question. Your function should return an integer corresponding to the knight’s minimum initial health required.

> 
> 
> 
> **Note:**
> 
> - The knight’s health has no upper bound.
> - Any room can contain threats or power-ups, even the first room the knight enters and the bottom-right room where the princess is imprisoned.

```cpp
int rec(int row,int col,vector<vector<int>> &dp,vector<vector<int> > &A){
     int m=A.size();
    int n=A[0].size();
    if(row>=m || col>=n){
        return INT_MIN;
    }
   
    int ans=0;
   
    if(row==m-1 && col==n-1){
        return min(0,ans+A[row][col]);
    }
    if(dp[row][col]!=-1){
        return dp[row][col];
    }
 
   
    ans=min(0,A[row][col]+max(rec(row+1,col,dp,A),rec(row,col+1,dp,A)));
    return dp[row][col]=ans;
}
int Solution::calculateMinimumHP(vector<vector<int> > &A) {
    int m=A.size();
    int n=A[0].size();
    vector<vector<int>> dp(m+1,vector<int>(n+1,-1));
    int ans=rec(0,0,dp,A);
    return abs(ans)+1;
}
```