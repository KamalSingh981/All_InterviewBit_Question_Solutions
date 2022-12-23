# Square Root of Integer | Interviewbit

Created: May 13, 2022 11:49 AM
URL: https://www.interviewbit.com/problems/square-root-of-integer/

**Problem Description**

Given an integer **A**.

Compute and return the **square root of A**.

If **A** is not a perfect square, return **floor(sqrt(A)).**

**DO NOT USE SQRT FUNCTION FROM STANDARD LIBRARY.**

**NOTE:** Do not use sort function from standard library. Users are expected to solve this in O(log(A)) time.

**Input Format**

The first and only argument given is the integer A.

**Output Format**

**Example Input**

**Example Output**

**Example Explanation**

Explanation:

```
 When A = 11 , square root of A = 3.316. It is not a perfect square so we return the floor which is 3.
 When A = 9 which is a perfect square of 3, so we return 3.

```

# Finding a number whose square is just equal to below the given number

```cpp
int Solution::sqrt(int A) {
    if (A == 1){
        return 1;
    }
    long long int low = 0, high = A/2;
    long long int mid = low + (high-low)/2;
    while(low<=high){
    mid = low + (high-low)/2;
    if(mid*mid<=A && ((mid+1)*(mid+1)>A)){
        return mid;
    }
    else if(mid*mid>A){
        high = mid -1;
    }
    else{
        low = mid + 1;
    }
    }
}
```