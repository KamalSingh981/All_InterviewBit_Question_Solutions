# Pairs With Given Xor | Interviewbit

Created: June 29, 2022 12:19 AM
Tags: Hashing
URL: https://www.interviewbit.com/problems/pairs-with-given-xor/

**Problem Description**

Given an 1D integer array **A** containing **N** distinct integers.

Find the number of unique pairs of integers in the array whose XOR is equal to **B**.

**NOTE:**

- Pair (a, b) and (b, a) is considered to be same and should be counted once.

**Problem Constraints**

1 <= N <= 105

1 <= A[i], B <= 107

**Input Format**

First argument is an 1D integer array **A**.

Second argument is an integer **B**.

**Output Format**

Return a single integer denoting the number of unique pairs of integers in the array **A** whose XOR is equal to **B**.

**Example Input**

Input 1:

```
 A = [5, 4, 10, 15, 7, 6]
 B = 5

```

Input 2:

```
 A = [3, 6, 8, 10, 15, 50]
 B = 5

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 (10 ^ 15) = 5

```

Explanation 2:

```
 (3 ^ 6) = 5 and (10 ^ 15) = 5

```

```cpp
int Solution::solve(vector<int> &A, int B) {
    int ans = 0;
    int cnt[1000001];
    for(int x:A){
        cnt[x]++;
    }
    for(int i = 0; i<A.size(); i++){
        ans += cnt[A[i]^B]*cnt[A[i]];
        cnt[A[i]] = cnt[A[i]^B] = 0;
    }
    return ans;
}
```

Find the first occurrence of an element in an array

```cpp
int firstOcc(int *a, int n, int key){
    if(n == 0){
        return -1;
    }
    if(a[0] == key){
        return 0;
    }

    int i = firstOcc(a+1, n-1, key);
    if(i == -1){
        return -1;
    }
    return i + 1;
}

// Second Code
int linearSearch(int *a, int i, int n, int key){
    if (i ==n){
        return -1;
    }
    if(a[i] == key){
        return i;
    }

    return linearSearch(a, i+1, n, key);
}
```