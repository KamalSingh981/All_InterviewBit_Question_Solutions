# Min Jumps Array | Interviewbit

Created: August 9, 2022 5:04 PM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/min-jumps-array/

Given an array of non-negative integers, **A**, of length **N**, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Return the **minimum** number of jumps required to reach the last index.

If it is not possible to reach the last index, return -1.

**Input Format:**

```
The first and the only argument contains an integer array, A.

```

**Output Format:**

```
Return an integer, representing the answer as described in the problem statement.

```

**Constraints:**

```
1 <= N <= 1e6
0 <= A[i] <= 50000

```

**Examples:**

```
Input 1:
    A = [2, 1, 1]

Output 1:
    1

Explanation 1:
    The shortest way to reach index 2 is
        Index 0 -> Index 2
    that requires only 1 jump.

Input 2:
    A = [2,3,1,1,4]

Output 2:
    2

Explanation 2:
    The shortest way to reach index 4 is
        Index 0 -> Index 1 -> Index 4
    that requires 2 jumps.

```

```cpp
int Solution::jump(vector<int> &arr) {
    int n=arr.size(), mx=0;

    if(n==1)
    return 0;

    if(arr[0]==0)
    return -1;

    int mx_reach=arr[0], step=arr[0], jump=1;

    for(int i=1; i<n; ++i)
    {
        if(i==n-1)
        return jump;

        mx_reach=max(mx_reach, i+arr[i]);

        step--;

        if(step==0)
        {
            jump++;
            step=mx_reach-i;
        }
    }
    return -1;
}
```

Dynamic Programming Solution O(N*k) where k is the size of element of the array.

```cpp
int tellTheFuckingAnswer(vector<int> &A, int k, vector<int> &dp){
    if(k>=A.size() - 1){
        return 0;
    }
       
    if(dp[k] != -1) return dp[k];   
    
    int ans = A.size() + 1;
    for(int i = 1; i<=A[k]; i++){
        if(k+i <= A.size())
        ans = min(ans,1+ tellTheFuckingAnswer(A, k+i, dp));
    }
    
    return dp[k] = ans;
}

int Solution::jump(vector<int> &A) {
        
    vector<int> dp(A.size()+1, -1);
    
    int ans =  tellTheFuckingAnswer(A, 0, dp);
    if(ans == A.size() + 1) return -1; 
    return ans;
}
```