# Combinations | Interviewbit

Created: July 12, 2022 10:43 PM
Tags: Backtracking, Recursion
URL: https://www.interviewbit.com/problems/combinations/

Given two integers `n` and `k`, return all possible combinations of `k` numbers out of `1 2 3 ... n`.

Make sure the combinations are **sorted**.

To elaborate,

1. Within every entry, elements should be sorted. `[1, 4]` is a valid entry while `[4, 1]` is not.
2. Entries should be sorted within themselves.

**Example :**
 If `n = 4` and `k = 2`, a solution is:

```
[
  [1,2],
  [1,3],
  [1,4],
  [2,3],
  [2,4],
  [3,4],
]

```

> 
> 
> 
> **Warning :** DO NOT USE LIBRARY FUNCTION FOR GENERATING COMBINATIONS. Example : itertools.combinations in python. *If you do, we will disqualify your submission retroactively and give you penalty points.*
> 

Done without help

```cpp
void findAllCombination(int A, int B, vector<vector<int>> &ans, int i, vector<int> a){    
    // Base Case
    if(B == 0){
        ans.push_back(a);
    }
     
    // Recursive Case
    for(int j = i; j<A; j++){
        if(a.size() == 0){
            a.push_back(j+1);
            findAllCombination(A, B - 1, ans, i+1, a);
            a.pop_back();
        }
        else if(a.back()<j+1){
            a.push_back(j+1);
            findAllCombination(A, B - 1, ans, i+1, a);
            a.pop_back();
        }
    }  
}

vector<vector<int> > Solution::combine(int A, int B) {
    vector<vector<int>> ans;
    vector<int> a;
    findAllCombination(A, B, ans, 0, a);
    return ans;
}
```

Interview Bit Code

```cpp
void dfs(vector<vector<int> >& ret, vector<int>& tmp, int n, int left, int k) {
    if (k == 0) {
        ret.push_back(tmp);
        return;
    }
    for (int i = left; i <= n; ++i) {
        tmp.push_back(i);
        dfs(ret, tmp, n, i + 1, k - 1);
        tmp.pop_back();
    }
}

vector<vector<int> > Solution::combine(int n, int k) {
    vector< vector<int> > ret;
    vector<int> tmp;
    dfs(ret, tmp, n, 1, k);
    return ret;
}
```