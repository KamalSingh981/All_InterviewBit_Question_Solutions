# Swap Bits | Interviewbit

Created: May 16, 2022 12:42 PM
Tags: bit manipullation
URL: https://www.interviewbit.com/problems/swap-bits/

**Problem Description**

Given an integer **A**.
Swap the **Bth** and **Cth** bit from right in binary representation of **A**.
Return the integer formed.

**Problem Constraints**

**Input Format**

First argument is an integer A.
Second argument is an integer B.
Third argument is an integer C.

**Output Format**

**Example Input**

Input 1:

```
A = 9
B = 1
C = 2

```

Input 2:

```
A = 1
B = 1
C = 3

```

**Example Output**

**Example Explanation**

Explanation 1:

```
5 -> 101
Swapping 1st and 2nd bit from right gives 110.

```

Explanation 2:

```
1 -> 001
Swapping 1st and 3rd bit from right gives 100.

```

```python
class Solution:
    # @param A : integer
    # @param B : integer
    # @param C : integer
    # @return an integer
    def solve(self, A, B, C):
        a = A
        i = 1
        b,c = 0,0
        while(A>0):
            if(i==B):
                b= A%2
            if(i == C):
                c = A%2
            i+=1
            A //=2
        if(b==1 and c==1 or b==0 and c==0):
            return a
        elif b==1 and c==0 or b==0 and c==1:
            a = (a^(1 << B-1))
            a = (a^ (1 << C-1))
            return a
```