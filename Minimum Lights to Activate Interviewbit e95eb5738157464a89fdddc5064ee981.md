# Minimum Lights to Activate | Interviewbit

Created: May 9, 2022 1:44 AM
URL: https://www.interviewbit.com/problems/minimum-lights-to-activate/

**Problem Description**

There is a corridor in a Jail which is **N** units long. Given an array **A** of size **N**. The **ith** index of this array is **0** if the light at ith position is faulty otherwise it is **1.**

All the lights are of specific power **B** which if is placed at position **X**, it can light the corridor from **[ X-B+1, X+B-1]**.

Initially all lights are off.

Return the **minimum number** of lights to be turned ON to light the whole corridor or **-1** if the whole corridor cannot be lighted.

**Problem Constraints**

**Input Format**

First argument is an integer array A where A[i] is either 0 or 1.

Second argument is an integer B.

**Output Format**

```
Return the minimum number of lights to be turned ON to light the whole corridor or -1 if the whole corridor cannot be lighted.
```

**Example Input**

Input 1:

```
A = [ 0, 0, 1, 1, 1, 0, 0, 1].
B = 3
```

Input 2:

```
A = [ 0, 0, 0, 1, 0].
B = 3
```

**Example Output**

Output 1:

```
2
```

Output 2:

```
-1
```

**Example Explanation**

Explanation 1:

```
In the first configuration, Turn on the lights at 3rd and 8th index.
Light at 3rd index covers from [ 1, 5] and light at 8th index covers [ 6, 8].
```

Explanation 2:

```
In the second configuration, there is no light which can light the first corridor.
```

```python
class Solution:
    # @param A : list of integers
    # @param B : integer
    # @return an integer
    def solve(self, A, B):
        count = 0
        a = len(A)
        i = 0
        while i<a:
            right = min(i + B-1, a-1)
            left = max(i - B +1, 0)
            flag = False
            while right>= left:
                if A[right] == 1:
                    flag = True
                    break
                right -=1
            if flag == False:
                return -1
            count += 1
            i = right + B
        return count
```