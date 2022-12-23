# Move Zeroes | Interviewbi

Created: May 9, 2022 1:36 AM
URL: https://www.interviewbit.com/problems/move-zeroes/

**Problem Description**

Given an integer array **A**, move all 0's to the end of it while maintaining the relative order of the non-zero elements.

Note that you must do this in-place without making a copy of the array.

**Problem Constraints**

**Input Format**

**Output Format**

**Example Input**

Input 1:

```
A = [0, 1, 0, 3, 12]

```

Input 2:

```
A = [0]

```

**Example Output**

Ouput 1:

```
[1, 3, 12, 0, 0]

```

Ouput 2:

```
[0]

```

**Example Explanation**

Explanation 1:

```
Shift all zeroes to the end.
```

Explanation 2:

```
There is only one zero so no need of shifting.

```

```cpp
vector<int> Solution::solve(vector<int> &A) {
    int count = 0;
    int l = A.size();
    for(int i =0; i<l; i++){
        A[count] = A[i];
        if (A[i]!=0){
            count += 1;
        }
    }
    for(int i = count; i<l; i++){
        A[i] = 0;
    }
    return A;
}
```