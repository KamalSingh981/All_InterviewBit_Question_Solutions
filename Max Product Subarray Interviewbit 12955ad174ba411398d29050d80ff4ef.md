# Max Product Subarray | Interviewbit

Created: August 1, 2022 10:37 PM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/max-product-subarray/

Find the contiguous subarray within an array (containing at least one number) which has the largest product.
 Return an integer corresponding to the maximum product possible.

**Example :**

```
Input : [2, 3, -2, 4]
Return : 6

Possible with [2, 3]

```

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
int Solution::maxProduct(const vector<int> &A) {
    int maxi = 1;
    int mini = 1;
    int ans = INT_MIN;
    for(int i  = 0; i<A.size(); i++){
        if(A[i] <0){
            swap(maxi, mini); // if we get a negative  number than after multiplying negative a maximum it will become minimum number similarly with maximum
        }
        maxi = max(A[i], maxi*A[i]); // stores the maximum element
        mini = min(A[i], mini*A[i]); // storest the minimum element
        ans = max(maxi, ans); // stores the answer
    }
    
    return ans;   
}
```