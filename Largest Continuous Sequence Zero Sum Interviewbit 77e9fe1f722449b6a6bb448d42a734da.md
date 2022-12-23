# Largest Continuous Sequence Zero Sum | Interviewbit

Created: July 15, 2022 1:49 AM
Tags: Hashing
URL: https://www.interviewbit.com/problems/largest-continuous-sequence-zero-sum/

Find the largest continuous sequence in a array which sums to zero.

**Example:**

> 
> 
> 
> **NOTE** : If there are multiple correct answers, return the sequence which occurs first in the array.
> 

```cpp
vector<int> Solution::lszero(vector<int> &A) {
        unordered_map<int, int> mp;
        int sum = 0;
        vector<int> res;
        int max_len = 0, s_i = -1, l_i = -1;
        mp[0] = -1;
        for (int i = 0; i < A.size(); i++)
        {
            sum += A[i];
            if (mp.find(sum) != mp.end())
            {
                if (i - mp[sum] > max_len)
                {
                    max_len = i - mp[sum];
                    s_i = mp[sum];
                    l_i = i;
                }
            }
            else
                mp[sum] = i;
        }
        for (int i = s_i + 1; i <= l_i; i++)
            res.push_back(A[i]);
        return res;
    }

    return max_len;
    
}
```