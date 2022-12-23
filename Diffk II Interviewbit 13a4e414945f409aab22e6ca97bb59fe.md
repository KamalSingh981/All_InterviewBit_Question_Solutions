# Diffk II | Interviewbit

Created: July 15, 2022 7:49 PM
Tags: Hashing
URL: https://www.interviewbit.com/problems/diffk-ii/

Given an array `A` of integers and another non negative integer `k`, find if there exists 2 indices `i` and `j` such that `A[i] - A[j] = k, i != j`.

**Example :**

Input :

```
A : [1 5 3]
k : 2

```

Output :

```
1

```

as `3 - 1 = 2`

- Return `0 / 1` for this problem.

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
int Solution::diffPossible(const vector<int> &A, int B) {
    
    if(A.size() == 1 or A.size() == 0){
        return 0;
    }
    unordered_map<int, int> m;
    for(int i= 0; i<A.size(); i++){
        m[A[i]]++;
    }
    
    for(int i= 0; i<A.size(); i++){
        if(m[A[i] + B]>0 && B != 0){
            
            return 1;
        }
        if(m[A[i] + B]>1){
            return 1;
            
        }
    }
    return 0;
}
```