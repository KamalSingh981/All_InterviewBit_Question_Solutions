# Sorted Insert Position | Interviewbit

Created: May 25, 2022 2:18 AM
Tags: Binary Search
URL: https://www.interviewbit.com/problems/sorted-insert-position/

**Problem Description**

Given a sorted array **A** and a target value **B**, return the index if the target is found. If not, return the index where it would be if it were inserted in order.

You may assume no duplicates in the array.

**Problem Constraints**

**Input Format**

First argument is array A.

Second argument is integer B.

**Output Format**

Return an integer, the answer to the problem.

**Example Input**

Input 1:

```
 A = [1, 3, 5, 6]
B = 5

```

Input 2:

```
 A = [1, 3, 5, 6]
B = 2

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 5 is found at index 2.

```

Explanation 2:

```
 2 will be inserted ar index 1.

```

```cpp
int Solution::searchInsert(vector<int> &A, int B) {
    // Do not write main() function.
    // Do not read input, instead use the arguments to the function.
    // Do not print the output, instead return values as specified
    // Still have a doubt. Checkout www.interviewbit.com/pages/sample_codes/ for more details
    int l = 0;
    int r = A.size();
    int mid;
    while(l<=r){
        mid = l + (r-l)/2;
        if(A[mid]<=B){
            l = mid +1;
        }
        else{
            r = mid -1;
        }
        if(A[mid] == B){
            return mid;
        }
    }
    return l;
}
```