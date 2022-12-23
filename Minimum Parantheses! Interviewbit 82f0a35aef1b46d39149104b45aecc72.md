# Minimum Parantheses! | Interviewbit

Created: May 17, 2022 10:24 AM
Tags: String
URL: https://www.interviewbit.com/problems/minimum-parantheses/

**Problem Description**

Given a string **A** of parantheses ‘(‘ or ‘)’.

The task is to find minimum number of parentheses ‘(‘ or ‘)’ (at any positions) we must add to make the resulting parentheses string valid.

An string is valid if:

- Open brackets must be closed by the corresponding closing bracket.
- Open brackets must be closed in the correct order.

**Problem Constraints**

1 <= |A| <= 105

A[i] = '(' or A[i] = ')'

**Input Format**

First and only argument is an string **A**.

**Output Format**

Return a single integer denoting the **minimum**number of parentheses ‘(‘ or ‘)’ (at any positions) we must add in **A** to make the resulting parentheses string valid.

**Example Input**

Input 1:

```
 A = "())"

```

Input 2:

```
 A = "((("

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 One '(' is required at beginning.

```

Explanation 2:

```
 Three ')' is required at end.

```

```python
class Solution:
    # @param A : string
    # @return an integer
    def solve(self, A):
        a, b = 0, 0
        for i in range(len(A)):
            if A[i] == ")":
                a += 1
                if b != 0:
                    a -= 1
                    b -= 1
            else:
                b += 1
        return a+b
```

Algorithm

In this question we are counting the “)” which do not have preceding “(”, if it is present then subtracting 1 from the “)” count as well as “(”, at last returning the sum of these two counts.