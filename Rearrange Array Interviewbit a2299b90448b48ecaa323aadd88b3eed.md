# Rearrange Array | Interviewbit

Created: May 22, 2022 2:24 AM
Tags: Math
URL: https://www.interviewbit.com/problems/rearrange-array/

Rearrange a given array so that `Arr[i]` becomes `Arr[Arr[i]]` with `O(1)` extra space.

**Example:**

```
Input : [1, 0]
Return : [0, 1]

```

> 
> 
> 
> Lets say `N` = `size of the array`. Then, following holds true :
> 
> - **All elements in the array are in the range `[0, N-1]`**
> - **`N * N` does not overflow for a signed integer**

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
void Solution::arrange(vector<int> &A) {
    int n = A.size();
     for(int i=0; i<A.size(); i++){
        A[i] = (A[A[i]]%n)*n + A[i];
    }
    for(int i=0; i<n; i++){
        A[i] = A[i]/n;
    }
}
```

Algorithm

We can encode two number information in a single digit if we know that both the numbers are less than n.

Let two numbers we want to encode a and b.

We can represents it as q = a*n + b, so while dividing q/n is equal to a and q%n = b.