# Distribute in Circle! | Interviewbit

Created: May 13, 2022 5:51 PM
URL: https://www.interviewbit.com/problems/distribute-in-circle/

**Problem Description**

**A** items are to be delivered in a circle of size **B**.

Find the position where the **Ath** item will be delivered if we start from a given position **C**.

**NOTE:** Items are distributed at adjacent positions starting from **C**.

**Problem Constraints**

**Input Format**

First argument is an integer **A**.

Second argument is an integer **B**.

Third argument is an integer **C**.

**Output Format**

Return an integer denoting the position where the **Ath** item will be delivered if we start from a given position **C**.

**Example Input**

Input 1:

```
 A = 2
 B = 5
 C = 1

```

Input 2:

```
 A = 8
 B = 5
 C = 2

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 The first item will be given to 1st position. Second (or last) item will be delivered to 2nd position

```

Explanation 2:

```
 The last item will be delivered to 4th position

```

```cpp
class Solution:
    # @param A : integer
    # @param B : integer
    # @param C : integer
    # @return an integer
    def solve(self, A, B, C):
        return (A + C - 1)%B;
```