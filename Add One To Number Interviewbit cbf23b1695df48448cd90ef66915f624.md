# Add One To Number | Interviewbit

Created: May 9, 2022 1:40 AM
URL: https://www.interviewbit.com/problems/add-one-to-number/

**Problem Description**

Given a **non-negative** number represented as an array of digits, add **1** to the number ( increment the number represented by the digits ).

The digits are stored such that the most significant digit is at the head of the list.

**NOTE:** Certain things are intentionally left unclear in this question which you should practice asking the interviewer. For example: for this problem, following are some good questions to ask :

- **Q :** Can the input have **0's** before the most significant digit. Or in other words, is **0 1 2 3** a valid input?
- **A :** For the purpose of this question, **YES**
- **Q :** Can the output have **0's** before the most significant digit? Or in other words, is **0 1 2 4** a valid output?
- **A :** For the purpose of this question, **NO**. Even if the input has zeroes before the most significant digit.

**Input Format**

First argument is an array of digits.

**Output Format**

Return the array of digits after adding one.

**Example Input**

**Example Output**

**Example Explanation**

Explanation 1:

```
Given vector is [1, 2, 3].
The returned vector should be [1, 2, 4] as 123 + 1 = 124.
```

```python
class Solution:
    # @param A : list of integers
    # @return a list of integers
    def plusOne(self, A):
        carry = 1
        for i in range(len(A)-1,-1,-1):
            d = A[i] + carry
            A[i] = d%10
            carry = d//10
        
        ans = []
        if carry!= 0:
                ans.append(carry)

        for i in range(len(A)):
            ans.append(A[i])

        count =0

        for j in range(len(ans)):
            count += 1
            if ans[j]!=0:
                break
      
        return ans[count-1:]
```