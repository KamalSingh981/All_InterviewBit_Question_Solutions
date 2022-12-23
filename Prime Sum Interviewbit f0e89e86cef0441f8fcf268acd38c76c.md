# Prime Sum | Interviewbit

Created: May 14, 2022 7:26 PM
URL: https://www.interviewbit.com/problems/prime-sum/

Given an even number ( greater than 2 ), return two prime numbers whose sum will be equal to given number.

**NOTE** A solution will always exist. read [Goldbach’s conjecture](https://en.wikipedia.org/wiki/Goldbach%27s_conjecture)

**Example:**

If there are more than one solutions possible, return the lexicographically smaller solution.

```
If [a, b] is one solution with a <= b,
and [c,d] is another solution with c <= d, then

[a, b] < [c, d]

If a < c OR a==c AND b < d.

```

```cpp
int isPrime(int n)
{
    for(int i=2;i<=sqrt(n);i++)
    {
        if(n%i==0) return false;
    }
    return true;
}

vector<int> Solution::primesum(int n) {
    vector<int> v;
    for(int i=2;i<=n/2;i++)
    {
        if( isPrime(i) && isPrime(n-i) )
        {
            v.push_back(i);
            v.push_back(n-i);
            return v;
        }
    }
}
```