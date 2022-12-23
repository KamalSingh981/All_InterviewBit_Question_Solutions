# K-th Permutation | Interviewbit

Created: July 14, 2022 1:29 AM
Tags: Backtracking
URL: https://www.interviewbit.com/problems/k-th-permutation/

**Problem Description**

You are given an integer **A** which represents the length of a permutation.
 A permutation is an array of length A where all the elements occur exactly once and in any order.
 For example, [3, 4, 1, 2], [1, 2, 3] are examples of valid permutations while [1, 2, 2], [2] are not.

You are also given an integer **B**.
 If all the permutation of length A are sorted lexicographically, return the Bth permutation.

**Problem Constraints**

1 <= A <= 105
 1 <= B <= min(1018, A!), where A! denotes the factorial of A.

**Input Format**

The first argument is the integer A.
 The second argument is the long integer B.

**Output Format**

**Example Input**

Input 1:

```
A = 3
B = 3

```

Input 2:

```
A = 1
B = 1

```

**Example Output**

Output 1:

```
[2, 1, 3]

```

Output 2:

```
[1]

```

**Example Explanation**

Explanation 1:

```
All the permutations of length 3 sorted in lexicographical order are:
[1, 2, 3], [1, 3, 2], [2, 1, 3], [2, 3, 1], [3, 1, 2], [3, 2, 1].
Therefore, the third permutation is [2, 1, 3].

```

Explanation 2:

```
There is only one possible permutation -> [1].

```

Interview Bit Code

```cpp
vector<int> Solution::findPerm(int A, long B) {
    vector<long>fact(21);
    fact[0] = 1;
    for (int i = 1; i <= 20; i++) {
        fact[i] = i * fact[i - 1];
    }
    vector<int> ans(A);
    int curr = 0;
    for (int i = 0; i < A - 20; i++) {
        ans[i] = i + 1;
        curr = i;
    }
    vector<int> l1;
    for (int i = max(A - 20, 1); i <= A; i++) {
        l1.push_back(i);
    }
    B--;
    for (int i = min(20, A - 1); i >= 0; i--) {
        int idx = (int)(B / fact[i]);
        B -= idx * fact[i];
        ans[curr++] = l1[idx];
        l1.erase(l1.begin() + idx);
    }
    return ans;
}
```