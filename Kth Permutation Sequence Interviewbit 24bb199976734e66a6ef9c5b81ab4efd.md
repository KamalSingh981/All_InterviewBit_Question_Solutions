# Kth Permutation Sequence | Interviewbit

Created: July 14, 2022 12:12 AM
Tags: Backtracking, Recursion
URL: https://www.interviewbit.com/problems/kth-permutation-sequence/

The set `[1,2,3,…,n]` contains a total of `n!` unique permutations.

By listing and labeling all of the permutations in order,
 We get the following sequence (ie, for `n = 3` ) :

```
1. "123"
2. "132"
3. "213"
4. "231"
5. "312"
6. "321"

```

Given n and k, return the kth permutation sequence.

For example, given `n = 3, k = 4, ans = "231"`

> 
> 
> 
> **Good questions to ask the interviewer :**
> 
> - What if n is greater than 10. How should multiple digit numbers be represented in string?
>     
>     > 
>     > 
>     > 
>     > In this case, just concatenate the number to the answer. so if `n = 11, k = 1, ans = "1234567891011"`
>     > 
> - Whats the maximum value of n and k?
>     
>     > 
>     > 
>     > 
>     > In this case, k will be a positive integer thats less than INT_MAX. n is reasonable enough to make sure the answer does not bloat up a lot.
>     > 

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
void ans(int n, int k, string &anst, vector<int> &arr, vector<int> &fact){
    if(n == 0) return;
    
    int f = fact[n-1];
    int  idx= k/f;
    if(k%f == 0){
        idx--;
    }
    anst += to_string(arr[idx]);
    arr.erase(arr.begin()+idx);
    k -= f*idx;
    ans(n-1, k, anst, arr, fact);
}

string Solution::getPermutation(int A, int B) {
    vector<int> s, fact(A+1, 1);
    for(int i = 1; i<=A; i++){
        s.push_back(i);
        if(i>12) fact[i] = INT_MAX;
        else fact[i] = i*fact[i-1];
        
    }
    
    string res = "";
    ans(A, B, res, s, fact);
    return res;
}
```