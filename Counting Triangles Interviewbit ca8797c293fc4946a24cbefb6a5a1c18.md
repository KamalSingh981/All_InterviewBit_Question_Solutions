# Counting Triangles | Interviewbit

Created: June 13, 2022 3:18 PM
Tags: Two pointers
URL: https://www.interviewbit.com/problems/counting-triangles/

You are given an array of **N** non-negative integers, **A0**, **A1** ,…, **AN-1**.
 Considering each array element **Ai** as the edge length of some line segment, count the number of triangles which you can form using these array values.

**Notes**:

1. 
    
    You can use any value only once while forming each triangle. Order of choosing the edge lengths doesn’t matter. Any triangle formed should have a positive area.
    
2. 
    
    Return answer modulo 109 + 7.
    

**For example**,

```
A = [1, 1, 1, 2, 2]

Return: 4

```

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
int Solution::nTriang(vector<int> &A) {
    sort(A.begin(), A.end());
    long long ans = 0;
    int mod = 1000000007;
    int n = A.size();
    for(int i = n - 1; i>= 2; i--){
        int st = 0;
        int en = i - 1;
        while(st<en){
            if(A[st] + A[en] > A[i]){
                ans += (en - st)%mod;
                en--;
            }
            else{
                st++;
            }
        }
    } 
    return ans%mod;
}
```

Explanation video

[https://www.youtube.com/watch?v=XGzCUpy_aFk](https://www.youtube.com/watch?v=XGzCUpy_aFk)