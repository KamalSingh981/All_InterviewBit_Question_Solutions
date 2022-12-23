# Maximum Substring | Interviewbit

Created: May 12, 2022 3:59 PM
URL: https://www.interviewbit.com/problems/maximum-substring/

**Problem Description**

Given a string **A** consisting of only characters 'a' and 'b'.
Divide the string into substrings of length **B**.
Find the subtring with maximum count of 'a' and return the count.

Note: If the length of the string is not a multiple of B and there are some characters left in the end consider them also as a substring.

**Problem Constraints**

**Input Format**

First argument A is a string.
Second argument is an integer B.

**Output Format**

**Example Input**

Input 1:

```
A = "baab"
B = 2

```

Input 2:

```
A = "bba"
B = 2

```

**Example Output**

**Example Explanation**

Explanation 1:

```
The subtrings are "ba" and "ab".
Both have count of 'a' equal to 1.
```

Explanation 2:

```
The substrings are "bb" and "a".
"a" has the highest count which is 1.
```

```python
class Solution:
    # @param A : string
    # @param B : integer
    # @return an integer
    def solve(self, A, B):  
        i = 0
        count = 0
        while(i<len(A)):
            count = max(A[i:i+B].count("a"), count)
            i += B

        count = max(A[i:].count("a"), count)
        return count
```