# Pascal Triangle | Interviewbit

Created: May 11, 2022 12:09 PM
URL: https://www.interviewbit.com/problems/pascal-triangle/submissions/

![Pascal%20Triangle%20Interviewbit%2047188ddef36944ff9619f32b1ed5876a/cover.9f999f.svg](Pascal%20Triangle%20Interviewbit%2047188ddef36944ff9619f32b1ed5876a/cover.9f999f.svg)

```python
class Solution:
    # @param A : integer
    # @return a list of list of integers
    def solve(self, A):
        ans = []
        for k in range(A):
            ans.append([1])
            ans[k][0] = 1;
            for i in range(1,k+1):
                ans[k].append(ans[k][i-1]*(k-i +1)//i);
        return ans
```