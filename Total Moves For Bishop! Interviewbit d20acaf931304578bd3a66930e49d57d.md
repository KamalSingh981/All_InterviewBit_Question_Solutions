# Total Moves For Bishop! | Interviewbit

Created: May 13, 2022 11:45 PM
URL: https://www.interviewbit.com/problems/total-moves-for-bishop/

**Problem Description**

Given the position of a Bishop **(A, B)** on an `8 * 8` chessboard.

Your task is to count the **total number of squares** that can be visited by the Bishop in one move.

The position of the Bishop is denoted using row and column number of the chessboard.

**Problem Constraints**

**Input Format**

First argument is an integer **A** denoting the row number of the bishop.

Second argument is an integer **B** denoting the column number of the bishop.

**Output Format**

Return an integer denoting the **total number of squares** that can be visited by the Bishop in one move.

**Example Input**

**Example Output**

```cpp
class Solution:
    # @param A : integer
    # @param B : integer
    # @return an integer
    def solve(self, A, B):
        ans  = min(A,B)-1 + min(A, 9-B)-1 + 8 - max(A, 9-B) + 8 - max(A,B) 
        return ans
```