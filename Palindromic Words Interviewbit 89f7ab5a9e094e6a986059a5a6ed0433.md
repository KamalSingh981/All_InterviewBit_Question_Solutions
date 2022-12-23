# Palindromic Words | Interviewbit

Created: May 9, 2022 2:00 AM
URL: https://www.interviewbit.com/problems/palindromic-words/

**Problem Description**

Given a sentence as a string **A**.
Return the number of **palindromic words** in the sentence.

**Problem Constraints**

**Input Format**

**Output Format**

**Example Input**

Input 1:

```
A = "the fastest racecar"

```

Input 2:

```
A = "wow mom"

```

**Example Output**

**Example Explanation**

Explanation 1:

```
The words are "hello" and "world".
12 + 34 = 46
```

Explanation 2:

```
The words are "how", "are" and "you".
```

```cpp
class Solution:
    # @param A : string
    # @return an integer
    def solve(self, A):
        ans = 0
        s = ""
        p = ""
        q = len(A)
        for i in range(q):
            if A[i] == " " or i==q-1:
                if i==q-1:
                    s = s+A[-1]
                p= ''.join(reversed(s))
                if p == s:
                    ans += 1
                s = ""
            else:
                s += A[i]
        return ans
```