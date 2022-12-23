# Ways to form Max Heap | Interviewbit

Created: July 18, 2022 4:06 PM
Tags: Heap
URL: https://www.interviewbit.com/problems/ways-to-form-max-heap/

**Problem Description**

**Max Heap** is a special kind of **complete binary tree** in which for every node the value present in that node is greater than the value present in it’s children nodes.

Find the number of **distinct Max Heap** can be made from **A distinct integers**.

In short, you have to ensure the following properties for the max heap :

- Heap has to be a complete binary tree ( A complete binary tree is a binary tree in which every level, except possibly the last, is completely filled, and all nodes are as far left as possible.)
- Every node is greater than all its children.

**NOTE:**  If you want to know more about Heaps, please visit this [link](https://en.wikipedia.org/wiki/Heap_%28data_structure%29). Return your answer **modulo 109 + 7**.

**Problem Constraints**

**Input Format**

First and only argument is an integer A.

**Output Format**

Return an integer denoting the number of distinct Max Heap.

**Example Input**

Input 1:

```
 A = 4
```

Input 2:

```
 A = 10
```

**Example Output**

Output 1:

```
 3
```

Output 2:

```
 3360
```

**Example Explanation**

Explanation 1:

```
 Let us take 1, 2, 3, 4 as our 4 distinct integers
 Following are the 3 possible max heaps from these 4 numbers :
      4           4                     4
    /  \         / \                   / \
   3    2   ,   2   3      and        3   1
  /            /                     /

 1            1                     2

```

Explanation 2:

```
 Number of distinct heaps possible with 10 distinct integers = 3360.

```

```cpp
#define ll long long 
#define M 1000000007
vector<vector<ll int>>nCrdp(101, vector<ll int>(101, -1));

ll int choose(ll int n, ll int r){
    if(r > n){     
        return 0;
    }
    if(n<=1) return 1;
    if(r == 0){
        return 1;
    }
    if(r == 1){
        return n;
    }
    if(nCrdp[n][r] != -1){
        return nCrdp[n][r];
    }
    ll int res = (choose(n-1, r -1) + choose(n -1, r))%M;
    nCrdp[n][r] =res;
    
    return res;
}

int NumofNodesOLeft(ll int n){
    int h = log2(n);
    int x =((1<<(h-1)) -1);
    int y = min((ll int)(1<<(h -1)), (n - ((1<<h)-1)));
    return x+y;
}

ll int getNumOfMaxHeaps(ll int n, vector<ll int> &dp){
    if(n <=1){
        return 1;
    }
    if(dp[n] != -1){
        return dp[n];
    }
    
    ll int L = NumofNodesOLeft(n);
    ll int waysToChosseL = choose(n-1,L)%M;
    ll int MaxHeapsUsingL = getNumOfMaxHeaps(L, dp)%M;
    ll int MaxHeapsUsingR = getNumOfMaxHeaps(n -1 -L, dp)%M;
    ll int ans = ((waysToChosseL%M)*((MaxHeapsUsingL*MaxHeapsUsingR)%M))%M;
    dp[n] = ans;
    return ans;
}

int Solution::solve(int A) {
    vector<ll int> dp(101, -1);
    return getNumOfMaxHeaps(A, dp);
    
    
}
```