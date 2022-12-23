# Prime Numbers | Interviewbit

Created: May 12, 2022 12:38 AM
URL: https://www.interviewbit.com/problems/prime-numbers/submissions/

![Prime%20Numbers%20Interviewbit%209cb08094f0b64d8abaaa4cfcbfc9adef/cover.9f999f.svg](Prime%20Numbers%20Interviewbit%209cb08094f0b64d8abaaa4cfcbfc9adef/cover.9f999f.svg)

```cpp
vector<int> Solution::sieve(int A) {
    bool prime[A + 1];
    memset(prime, true, sizeof(prime));

    for (int p = 2; p * p <= A; p++) {
        if (prime[p] == true) {
            for (int i = p * p; i <= A; i += p)
                prime[i] = false;
        }
    }

    vector<int> ans;
    for (int p = 2; p <= A; p++) {
        if (prime[p]) {
            ans.push_back(p);
        }
    }
    return ans;
}
```