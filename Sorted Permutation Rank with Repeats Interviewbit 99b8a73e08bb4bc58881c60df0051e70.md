# Sorted Permutation Rank with Repeats | Interviewbit

Created: May 23, 2022 2:02 AM
Tags: MMI, Math, Very Hard Question
URL: https://www.interviewbit.com/problems/sorted-permutation-rank-with-repeats/

Given a string, find the rank of the string amongst its permutations sorted lexicographically. 
 Note that the characters might be repeated. If the characters are repeated, we need to look at the rank in unique permutations. 
 Look at the example for more details.

**Example :**

The answer might not fit in an integer, so return `your answer % 1000003`

> 
> 
> 
> **NOTE:** 1000003 is a prime number **NOTE:** Assume the number of characters in string < 1000003
> 

```cpp
int mod = 1000003;

long long power(long long x, long long y)
{
    long long res = 1;
    while (y > 0) {
        if (y & 1ll)
            res = (res * x) % mod;
        y = y >> 1;
        x = (x * x) % mod;
    }
    return res;
}
int inverse(int a)
{
    return power(a, mod - 2);
}

int Solution::findRank(string A) {
    
    multiset<char> s(A.begin(), A.end());
    long long ans = 0;

    map<char,int> f;
    for(char c : A) f[c]++;

    int n = A.size();
    vector<int> fact(n+1, 1);

    for(int i = 1; i<=n; i++) fact[i] = fact[i-1] * i, fact[i] %= mod;
    for(int i = 0; i<n; i++)
    {
        char smallest = *s.begin();
        char curr = A[i];
        for(char c = smallest; c < curr; c++)
        {
            if(f[c])
            {
                f[c]--;
                long long sum = 0;
                long long temp = 1;
                for(auto [c1, freq] : f)
                {
                    sum += freq;
                    temp *= inverse(fact[freq]), temp %= mod;
                }
                temp *= fact[sum];
                temp %= mod;
                ans += temp;
                ans %= mod;
                f[c]++;
            }
        }
        f[curr]--;
        s.erase(s.find(curr));
    }

    return (ans+1) % mod;
}
```