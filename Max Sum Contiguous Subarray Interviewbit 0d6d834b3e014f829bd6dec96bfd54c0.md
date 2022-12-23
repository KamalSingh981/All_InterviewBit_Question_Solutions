# Max Sum Contiguous Subarray | Interviewbit

Created: May 11, 2022 11:29 AM
URL: https://www.interviewbit.com/problems/max-sum-contiguous-subarray/

Find the **contiguous** subarray within an array, **A** of length **N** which has the **largest sum**.

**Input Format:**

```
The first and the only argument contains an integer array, A.

```

**Output Format:**

```
Return an integer representing the maximum possible sum of the contiguous subarray.

```

**Constraints:**

```
1 <= N <= 1e6
-1000 <= A[i] <= 1000

```

**For example:**

```
Input 1:
    A = [1, 2, 3, 4, -10]

Output 1:
    10

Explanation 1:
    The subarray [1, 2, 3, 4] has the maximum possible sum of 10.

Input 2:
    A = [-2, 1, -3, 4, -1, 2, 1, -5, 4]

Output 2:
    6

Explanation 2:
    The subarray [4,-1,2,1] has the maximum possible sum of 6.

```

```python
int Solution::maxSubArray(const vector<int> &A) {
    int maxsum = 0;
    int ans = INT_MIN;
    for(int k =0; k<A.size(); k++){
        maxsum += A[k];
        ans = max(ans, maxsum);
        if(maxsum<0){
            maxsum = 0;
        }       
    }
    return ans;
}
```