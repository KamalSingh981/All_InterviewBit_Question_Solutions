# Rain Water Trapped | Interviewbit

Created: June 19, 2022 8:04 PM
Tags: Stacks
URL: https://www.interviewbit.com/problems/rain-water-trapped/

**Problem Description**

Given an integer array **A** of non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

**Problem Constraints**

**Input Format**

The only argument given is integer array A.

**Output Format**

Return the total water it is able to trap after raining.

**Example Input**

Input 1:

```
 A = [0, 1, 0, 2, 1, 0, 1, 3, 2, 1, 2, 1]

```

Input 2:

```
 A = [1, 2]

```

**Example Output**

**Example Explanation**

Explanation 1:

```
In this case, 6 units of rain water (blue section) are being trapped.
```

![Rain%20Water%20Trapped%20Interviewbit%20fe4d11123b9f4c3daad1774729bb5d8c/BMA6YRo.jpeg](Rain%20Water%20Trapped%20Interviewbit%20fe4d11123b9f4c3daad1774729bb5d8c/BMA6YRo.jpeg)

Explanation 2:

```
 No water is trapped.

```

```cpp
int Solution::trap(const vector<int> &A) {
    int n = A.size();
    vector<int> pref(n);
    vector<int> suff(n);
    pref[0] = A[0];
    suff[n-1] = A[n-1];
    for(int i = 1; i<n; i++){
        pref[i]  = max(pref[i-1], A[i]);
        suff[n-i-1] = max(suff[n-i], A[n-i-1]);
    }
    int ans = 0;
    for(int i = 0; i<n; i++){
        ans += abs(min(pref[i], suff[i]) - A[i]);
    }
    return ans;
}
```