# Maximum Area of Triangle! | Interviewbit

Created: May 17, 2022 2:00 AM
Tags: Very Hard Question
URL: https://www.interviewbit.com/problems/maximum-area-of-triangle/

**Problem Description**

Given a character matrix of size `N x M` in the form of a string array **A** of size **N** where A[i] denotes ith row.

Each character in the matrix consists any one of the following three characters {'r', 'g', 'b'} where **'r'** denotes **red** color similarly **'g'** denotes **green** color and **'b'** denotes **blue** color.

You have to find the area of the **largest triangle** that has one side parallel to y-axis i.e vertical and the color of all three vertices are different.

**NOTE:**

- If the area comes out to be a real number than return the [ceil](https://en.wikipedia.org/wiki/Floor_and_ceiling_functions) of that number.

**Problem Constraints**

2 <= N, M <= 103

A[i][j] = 'r' or A[i][j] = 'g' or A[i][j] = 'b'

**Input Format**

First and only argument is an string array **A** of size **N** denoting the 2D character matrix.

**Output Format**

Return a single integer denoting the area of the **largest triangle** that has one side parallel to y-axis i.e vertical and the color of all three vertices are different.

If the area comes out to be a real number than return the [ceil](https://en.wikipedia.org/wiki/Floor_and_ceiling_functions) of that number.

**Example Input**

Input 1:

```
 A = ["rrrrr", "rrrrg", "rrrrr", "bbbbb"]

```

Input 2:

```
 A = ["rrr", "rrr", "rrr", "rrr"]

```

**Example Output**

Output 1:

```
 10

```

Output 2:

```
 0

```

**Example Explanation**

Explanation 1:

```
 The maximum area of triangle is 10.
 Triangle coordinates are (0,0) containing r, (1,4) containing g, (3,0) containing b.

```

![Maximum%20Area%20of%20Triangle!%20Interviewbit%20f28420947fab4871a784edc6c7e8b3b0/DnNR1Vp.jpeg](Maximum%20Area%20of%20Triangle!%20Interviewbit%20f28420947fab4871a784edc6c7e8b3b0/DnNR1Vp.jpeg)

Explanation 2:

```
 All cells have same color so no triangle possible so we will return 0

```

```python
class Solution:
    # @param A : list of strings
    # @return an integer
    def solve(self, A):
        R = len(A)
        C = len(A[0])
        ret = 0
        for i in range(C):
            f = False
            for j in range(R):
                while j < R and j != 0 and A[j][i] == A[j-1][i]:
                    j += 1
                if j == R:
                    break
                c1 = A[j][i]
                for k in range(R-1, j, -1):
                    if A[k][i] != c1:
                        c2 = A[k][i]
                        for l in range(C-1, i-1, -1):
                            for m in range(R):
                                if A[m][l] != c1 and A[m][l] != c2:
                                    ret = max(ret, math.ceil((abs(l-i)+1) * (abs(k-j)+1) / 2))
                                    f = True
                                    break
                            if f:
                                break
                    if f:
                        break
                if f:
                    break
            if f:
                break
                                
        for i in range(C-1, -1, -1):
            f = False
            for j in range(R):
                while j< R and j != 0 and A[j][i] == A[j-1][i]:
                    j += 1
                if j == R:
                    break
                c1 = A[j][i]
                for k in range(R-1, j, -1):
                    if A[k][i] != c1:
                        c2 = A[k][i]
                        for l in range(i+1):
                            f = False
                            for m in range(R):
                                if A[m][l] != c1 and A[m][l] != c2:
                                    ret = max(ret, math.ceil((abs(l-i)+1) * (abs(k-j)+1) / 2))
                                    f = True
                                    break
                            if f:
                                break
                    if f:
                        break
                if f:
                    break
            if f:
                break
                                
        return ret
```