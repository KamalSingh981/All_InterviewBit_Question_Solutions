# NUMRANGE | Interviewbit

Created: July 17, 2022 2:29 AM
Tags: Math, Two pointers
URL: https://www.interviewbit.com/problems/numrange/

Given an array of **non negative** integers `A`, and a range `(B, C)`, 
 find the number of continuous subsequences in the array which have sum `S` in the range `[B, C]` or `B <= S <= C`

Continuous subsequence is defined as all the numbers `A[i], A[i + 1], .... A[j]`
 where `0 <= i <= j < size(A)`

**Example :**

```
A : [10, 5, 1, 0, 2]
(B, C) : (6, 8)

```

ans = 3 
 as `[5, 1], [5, 1, 0], [5, 1, 0, 2]` are the only 3 continuous subsequence with their sum in the range [6, 8]

> 
> 
> 
> **NOTE :** The answer is guranteed to fit in a 32 bit signed integer.
> 

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
int Solution::numRange(vector<int> &A, int B, int C) {
    int l = 0;
    int r = 0;
    int currsum = 0;
    int ans = 0;
    while(r<A.size()){
        currsum  += A[l];
        if((currsum >=B) and (currsum<=C)){
            ans++;
            l++;
        }
        else if(currsum < B){
            l++;
        }
        else if(currsum>C){
            r++;
            l = r;
            currsum = 0;      
        } 
        if(l == A.size()){
            currsum = 0;
            r++;
            l = r;
        }       
    }
    return ans;
}
```