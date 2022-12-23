# Kth Row of Pascal's Triangle | Interviewbit

Created: May 11, 2022 11:42 AM
URL: https://www.interviewbit.com/problems/kth-row-of-pascals-triangle/

**Problem Description**

Given an index k, return the kth row of the Pascal's triangle.

Pascal's triangle: To generate A[C] in row R, sum up A'[C] and A'[C-1] from previous row R - 1.

**Example:**

```
Input : k = 3

Return : [1,3,3,1]

```

**Note**: k is 0 based. k = 0, corresponds to the row [1].

**Note**: Could you optimize your algorithm to use only O(k) extra space?

```python
vector<int> Solution::getRow(int A) {
    vector<int> ans;
    ans.push_back(1);
    int pre = 1;
    for(int i=1; i<=A; i++){
        ans.push_back(ans[i-1]*(A-i +1)/i);
    }
    return ans;
}
```