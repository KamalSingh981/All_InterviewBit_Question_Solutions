# XOR-ing the Subarrays! | Interviewbit

Created: June 16, 2022 12:53 AM
Tags: bit manipullation
URL: https://www.interviewbit.com/problems/xor-ing-the-subarrays/

**Problem Description**

Given an integer array **A** of size **N**.

You need to find the value obtained by [XOR](https://en.wikipedia.org/wiki/Exclusive_or)-ing the contiguous subarrays, followed by [XOR](https://en.wikipedia.org/wiki/Exclusive_or)-ing the values thus obtained. Determine and return this value.

For example, if A = [3, 4, 5] :

```
Subarray    Operation   Result
3       None            3
4       None            4
5       None            5
3,4   3 XOR 4         7
4,5   4 XOR 5         1
3,4,5    3 XOR 4 XOR 5   2

```

Now we take the resultant values and XOR them together:

3 ⊕ 4 ⊕ 5 ⊕ 7 ⊕ 1⊕ 2 = 6 we will return 6.

**Problem Constraints**

**Input Format**

First and only argument is an integer array **A**.

**Output Format**

Return a single integer denoting the value as described above.

**Example Input**

Input 1:

```
 A = [1, 2, 3]

```

Input 2:

```
 A = [4, 5, 7, 5]

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 1 ⊕ 2 ⊕ 3 ⊕  (1 ⊕ 2 ) ⊕ (2 ⊕ 3) ⊕ (1 ⊕ 2 ⊕ 3) = 2

```

Explanation 2:

```
 4 ⊕ 5 ⊕ 7 ⊕ 5 ⊕ (4 ⊕ 5) ⊕ (5 ⊕ 7) ⊕ (7 ⊕ 5) ⊕ (4 ⊕ 5 ⊕ 7) ⊕ (5 ⊕ 7 ⊕ 5) ⊕ (4 ⊕ 5 ⊕ 7 ⊕ 5) = 0

```

```python
int Solution::solve(vector<int> &A) {
    if(A.size()%2 == 0){
        return 0;
    }
    int ans = 0;
    for(int i=0; i<A.size(); i += 2){
        ans  = ans^A[i];
    }
    return ans;
}
```