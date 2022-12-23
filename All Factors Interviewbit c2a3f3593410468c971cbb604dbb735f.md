# All Factors | Interviewbit

Created: May 11, 2022 11:27 AM
URL: https://www.interviewbit.com/problems/all-factors/

Given a number N, find all factors of N.

**Example:**

Make sure the returned array is sorted.

**Problem Approach:**

VIDEO : https://www.youtube.com/watch?v=dolcMgiJ7I0

Complete code in the hint.

```python
#include <list>
vector<int> Solution::allFactors(int A) {
    int d = sqrt(A);
    vector<int> ans;
    for(int i=1; i<=d; i++){
        if(A%i==0){
            if(A/i==i){
                ans.push_back(i);
            }
            else{
                ans.push_back(i);
                ans.push_back(A/i);
            }
        }
    }
    sort(ans.begin(), ans.end());

    return ans;
}
```