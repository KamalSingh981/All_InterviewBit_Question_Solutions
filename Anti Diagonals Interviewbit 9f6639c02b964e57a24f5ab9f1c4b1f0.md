# Anti Diagonals | Interviewbit

Created: May 11, 2022 1:49 PM
URL: https://www.interviewbit.com/problems/anti-diagonals/

**Problem Description**

Give a N*N square matrix, return an array of its anti-diagonals. Look at the example for more details.

**Example:**

```
Input:

1 2 3
4 5 6
7 8 9
Return the following:
[
  [1],
  [2, 4],
  [3, 5, 7],
  [6, 8],
  [9]
]

Input:
1 2
3 4
Return the following:
[
  [1],
  [2, 3],
  [4]
]

```

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

### My code

```python
class Solution:
    # @param A : list of list of integers
    # @return a list of list of integers
    def diagonal(self, A):
        p = len(A) - 1
        ans = [[A[0][0]]]
        if(p==0):
            return ans
        else:
            for d in range(2):
                if (d == 0):
                    i = 0
                    j = 0
                    for q in range(1, p + 1):
                        j += 1
                        c = j
                        r = i+1
                        ans.append([A[i][j]])
                        while (0!=j and i!=c):
                            i += 1
                            j -= 1
                            ans[q].append(A[i][j])
                        j = c
                        i = 0
                else:
                    i = 0
                    j = p
                    for q in range(1, p):
                        i += 1
                        c = i
                        r = j + 1
                        ans.append([A[i][j]])
                        while (0 != j and i != p):
                            i += 1
                            j -= 1
                            ans[c+p].append(A[i][j])
                        j = p
                        i = c
            ans.append([A[p][p]])

        return ans
```

## Interview bit code

```python
class Solution:
    # @param A : list of list of integers
    # @return a list of list of integers
    def diagonal(self, A):
        n=len(A)
        ans=[[] for i in range(2*n-1)]
        for i in range(n):
            for j in range(n):
                ans[i+j].append(A[i][j])
        return ans
```