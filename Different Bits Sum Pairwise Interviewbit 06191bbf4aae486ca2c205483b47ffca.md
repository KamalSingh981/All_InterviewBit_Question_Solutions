# Different Bits Sum Pairwise | Interviewbit

Created: June 16, 2022 1:27 AM
Tags: bit manipullation
URL: https://www.interviewbit.com/problems/different-bits-sum-pairwise/

We define `f(X, Y)` as number of different corresponding bits in binary representation of X and Y. For example, `f(2, 7)` = 2, since binary representation of 2 and 7 are `010` and `111`, respectively. The first and the third bit differ, so `f(2, 7)` = 2.

You are given an array of N positive integers, A1, A2 ,…, AN. Find sum of f(Ai, Aj) for all pairs (i, j) such that 1 ≤ i, j ≤ N. Return the answer modulo 109+7.

For example,

```
A=[1, 3, 5]

We return

f(1, 1) + f(1, 3) + f(1, 5) +
f(3, 1) + f(3, 3) + f(3, 5) +
f(5, 1) + f(5, 3) + f(5, 5) =

0 + 1 + 1 +
1 + 0 + 2 +
1 + 2 + 0 = 8

```

```python
int Solution::cntBits(vector<int> &A) {
    long long mod = 1000000007;
    long long ans = 0;
    for(int i = 0; i<32; i++){
        long long int ones = 0;
        long long zero = 0;
        for(int j =0; j<A.size(); j++){
            if(A[j]&(1<<i)){
                ones++;
            }
            else{
                zero++;
            }
        }
        ans += (ones*(zero)*2)%mod;
    }
    return ans%mod;
}
```