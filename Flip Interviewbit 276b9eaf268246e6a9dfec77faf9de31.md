# Flip | Interviewbit

Created: May 15, 2022 11:47 PM
URL: https://www.interviewbit.com/problems/flip/

**Problem Description**

You are given a binary string **A**(i.e. with characters **0** and **1**) consisting of characters **A1**, **A2**, ..., **AN**. In a single operation, you can choose two indices **L** and **R** such that **1** ≤ **L** ≤ **R** ≤ **N** and flip the characters **AL**, **AL+1**, ..., **AR**. By flipping, we mean change character **0** to **1** and vice-versa.

Your aim is to perform **ATMOST** one operation such that in final string number of **1s** is maximised.

If you don't want to perform the operation, return an **empty** array. Else, return an array consisting of two elements denoting **L** and **R**. If there are multiple solutions, return the **lexicographically smallest** pair of **L** and **R**.

**NOTE:** Pair **(a, b)** is lexicographically smaller than pair **(c, d)** if **a** < **c** or, if **a** == **c** and **b** < **d**.

**Input Format**

**Output Format**

**Example Input**

Input 1:

```
A = "010"
```

Input 2:

```
A = "111"
```

**Example Output**

**Example Explanation**

Explanation 1:

```
A = "010"

Pair of [L, R] | Final string
____________|__________
[1 1]          | "110"
[1 2]          | "100"
[1 3]          | "101"
[2 2]          | "000"
[2 3]          | "001"We see that two pairs [1, 1] and [1, 3] give same number of 1s in final string. So, we return [1, 1].

```

Explanation 2:

```
No operation can give us more than three 1s in final string. So, we return empty array [].
```

```python
class Solution:
    # @param A : string
    # @return a list of integers
    def flip(self, A):
        l = 0
        pair = []
        max_ones = 0
        curr_ones = 0
        for r in range(len(A)):
            
            if A[r] == '0':
                curr_ones += 1
                
                if curr_ones > max_ones:
                    max_ones = curr_ones
                    pair = [l+1, r+1]
                    
            else:
                curr_ones -= 1
                if curr_ones < 0:
                    l = r+1
                    curr_ones = 0
        return pair
```

In this question we can find the difference in 0’s and 1’s after flipping the subarray by converting 0’s by -1’s and 1 by 1 and then finding the sum of that array will give A-B.

After that we can simply apply kadane’s algorithm.