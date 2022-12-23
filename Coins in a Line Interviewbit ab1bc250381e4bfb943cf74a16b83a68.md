# Coins in a Line | Interviewbit

Created: August 9, 2022 12:29 AM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/coins-in-a-line/

**Problem Description**

There are **A** coins (Assume A is even) in a line.

Two players take turns to take a coin from one of the ends of the line until there are no more coins left.

The player with the larger amount of money wins, Assume that you go first.

Return the **maximum amount** of money you can win.

**NOTE:**

- You can assume that opponent is clever and plays optimally.

**Problem Constraints**

**Input Format**

The first and the only argument of input contains an integer array **A**.

**Output Format**

Return an integer representing the maximum amount of money you can win.

**Example Input**

Input 1:

```
 A = [1, 2, 3, 4]

```

Input 2:

```
 A = [5, 4, 8, 10]

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 You      : Pick 4
 Opponent : Pick 3
 You      : Pick 2
 Opponent : Pick 1

Total money with you : 4 + 2 = 6

```

Explanation 2:

```
 You      : Pick 10
 Opponent : Pick 8
 You      : Pick 5
 Opponent : Pick 4

Total money with you : 10 + 5 = 15

```

```cpp
int findMyFuckingAnswer(vector<int> &A, int i, int j, int turn,vector<vector<vector<int>>> &dp){
    
    if(i>j){
        return 0;
    }
    
    if(dp[i][j][turn] != -1) return dp[i][j][turn];
    
    int ans;
    
    if(turn){
        ans = max(A[i] + findMyFuckingAnswer(A, i+1, j, 0,dp), A[j] + findMyFuckingAnswer(A, i, j-1, 0, dp));
    }
    else{
        ans = min(findMyFuckingAnswer(A, i + 1, j , 1, dp), findMyFuckingAnswer(A, i, j-1, 1, dp));
    }
    return dp[i][j][turn] = ans;
    
    
    
}

int Solution::maxcoin(vector<int> &A) {
    
    vector<vector<vector<int>>> dp(A.size(), vector<vector<int>> (A.size(), vector<int>(2, -1)));
    return findMyFuckingAnswer(A, 0, A.size() - 1, 1, dp);
}
```

```cpp
int rec(vector<int> &a,int i,int j,vector<vector<int> > &m)
{
    if(j<i) return 0;
    if(i==j) return a[i];
    if(i+1==j) return max(a[i],a[j]);
    if(m[i][j]!=-1) return m[i][j];
    return m[i][j]=max(a[i]+min( rec(a,i+2,j,m) , rec(a,i+1,j-1,m) ),a[j]+min( rec(a,i+1,j-1,m),rec(a,i,j-2,m) ) );
}
int Solution::maxcoin(vector<int> &a) {
    vector<vector<int> > m(a.size(),vector<int> (a.size(),-1));
    return rec(a,0,a.size()-1,m);   
}
```