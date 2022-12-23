# Egg Drop Problem! | Interviewbit

Created: August 6, 2022 12:15 PM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/egg-drop-problem/

**Problem Description**

You are given **A** eggs, and you have access to a building with **B** floors from **1** to **B**.

Each egg is identical in function, and if an egg breaks, you cannot drop it again.

You know that there exists a floor **C** with **0 <= C <= B**  such that any egg dropped at a floor higher than **C** will break, and any egg dropped at or below floor **C** will not break.

Each move, you may take an egg (if you have an unbroken one) and drop it from any floor **X** (with **1 <= X <= B**).

Your goal is to know with certainty what the value of **C** is.

What is the minimum number of moves that you need to know with certainty what **C** is, regardless of the initial value of **C**

**Problem Constraints**

**Input Format**

First Argument is an integer **A** denoting number of eggs.

Second Argument is an integer **B** denoting number of floors.

**Output Format**

Return an integer denoting the Minimum number of moves.

**Example Input**

Input 1:

```
 A = 1
 B = 2

```

Input 2:

```
 A = 2
 B = 10

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 Drop the egg from floor 1.  If it breaks, we know with certainty that F = 0.
 Otherwise, drop the egg from floor 2.  If it breaks, we know with certainty that F = 1.
 If it didn't break, then we know with certainty F = 2.
 Hence, we needed 2 moves in the worst case to know what F is with certainty.

```

```cpp
int tellTheAnswer(int i, int j, vector<vector<int>> &dp){
    if(j == 0) return 0;
    if(i ==0) return 1e9;
    
    if(dp[i][j] != -1){
        return dp[i][j];
    }
    
    int mini = 1e9;
    int lo = 1, hi = j;
    
    while(lo <= hi){
        int mid = (lo + hi)/2;
        int f1 = tellTheAnswer(i-1, mid -1, dp);
        int f2 = tellTheAnswer(i, j - mid, dp);
        mini = min(mini, 1 + max(f1, f2));
        
        if(f2>f1){
            lo = mid+1;
        }
        else{
            hi = mid - 1;
        }
    }
    
    return dp[i][j] = mini;
}

int Solution::solve(int A, int B) {
    vector<vector<int>> dp(A +1, vector<int>(B + 1, -1));
    return tellTheAnswer(A, B, dp);
}
```