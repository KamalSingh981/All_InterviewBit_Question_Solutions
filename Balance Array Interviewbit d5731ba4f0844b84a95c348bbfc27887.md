# Balance Array | Interviewbit

Created: May 12, 2022 1:37 PM
URL: https://www.interviewbit.com/problems/balance-array/

**Problem Description**

Given an integer array **A** of size **N**. You need to count the number of **special** elements in the given array.

A element is **special** if removal of that element make the array **balanced**.

Array will be **balanced** if sum of **even** index element **equal** to sum of **odd** index element.

**Problem Constraints**

1 <= N <= 105

1 <= A[i] <= 109

**Input Format**

First and only argument is an integer array A of size N.

**Output Format**

Return an integer denoting the count of special elements.

**Example Input**

Input 1:

```
 A = [2, 1, 6, 4]
```

Input 2:

```
 A = [5, 5, 2, 5, 8]
```

**Example Output**

**Example Explanation**

Explanation 1:

```
 After deleting 1 from array : {2,6,4}
    (2+4) = (6)
 Hence 1 is the only special element, so count is 1
```

Explanation 2:

```
 If we delete A[0] or A[1] , array will be balanced
    (5+5) = (2+8)
 So A[0] and A[1] are special elements, so count is 2.
```

```cpp
int Solution::solve(vector<int> &A) {
    int n = A.size();
    int odd = 0, even = 0;
    int leftOdd[n], rightOdd[n];
    int leftEven[n], rightEven[n];
    for(int i = 0;i < n; i++){
        leftOdd[i] = odd;
        leftEven[i] = even;
        if(i%2 == 0)
            even += A[i];
        else
            odd += A[i];
    }
    odd = 0;
    even = 0;
    for(int i = n-1; i >= 0; i--){
        rightOdd[i] = odd;
        rightEven[i] = even;
        if(i%2 == 0)
            even += A[i];
        else
            odd += A[i];
    }
    int ans = 0;
    for(int i = 0; i < n; i++){
        if(leftOdd[i] + rightEven[i] == leftEven[i] + rightOdd[i]){
            ans++;
        }
    }
    return ans;

}
```