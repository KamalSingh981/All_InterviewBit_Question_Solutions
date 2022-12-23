# Potions | Interviewbit

Created: August 6, 2022 1:56 AM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/potions/

**Problem Description**

You are given **N** potions arranged in a row in the form of an array **A**.
 Each potion has one of 100 different colors (colors have numbers from 0 to 99).
 You need to mix all these potions together.
 At each step, you are going to take two potions that stand next to each other and mix them together,
 and put the resulting mixture in their place.
 When mixing two mixtures of colors **X** and **Y**, the resulting mixture will have the color **(X + Y) mod 100**.
 Also, there will be some smoke in the process. The amount of smoke generated when mixing two mixtures of colors X and Y is **X * Y**.
 Find out what is the minimum amount of smoke that you can get when mixing all the potions together.

**Problem Constraints**

**Input Format**

**Output Format**

**Example Input**

Input 1:

```
A = [2, 3]

```

Input 2:

```
A = [2, 3, 4, 5]

```

**Example Output**

Output 1:

```
6

```

Output 2:

```
71

```

**Example Explanation**

Explanation 1:

```
There are only two potions given. Upon mixing them, we get 2 * 3 = 6 amounts of smoke.
```

Explanation 2:

```
Out of all the possible order of operations of mixing the given potions, the minimum amount of smoke you can get is 71.

```

```cpp
long long sum(int i, int j, vector<int> &A){
    long long ans = 0;
    for(int k = i; k<=j; k++){
        ans += A[k];
        ans %=100;
    }
    return ans;
}

long long findsmoke(vector<int> &A, int i, int j,vector<vector<long long>> &dp){
    if(i>=j) return 0;
    if(dp[i][j] != -1) return dp[i][j];
    
    dp[i][j] = INT_MAX;
    for(int k = i; k<=j; k++){
        dp[i][j] = min(dp[i][j], (findsmoke(A, i, k, dp) + findsmoke(A, k + 1, j, dp) + sum(i, k, A)*sum(k+1, j, A)));
    }
    return dp[i][j];
}

int Solution::minSmoke(vector<int> &A) {
    vector<vector<long long>> dp(110, vector<long long>(110, -1));
    return findsmoke(A, 0, A.size()-1, dp);
}
```