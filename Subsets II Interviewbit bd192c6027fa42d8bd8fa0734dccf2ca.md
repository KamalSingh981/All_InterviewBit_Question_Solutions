# Subsets II | Interviewbit

Created: July 12, 2022 11:22 PM
Tags: Backtracking, Recursion
URL: https://www.interviewbit.com/problems/subsets-ii/

Given a collection of integers that might contain duplicates, `S`, return all possible subsets.

> 
> 
> 
> **Note:**
> 
> - Elements in a subset must be in non-descending order.
> - The solution set must not contain duplicate subsets.
> - The subsets must be sorted lexicographically.

**Example :**
 If `S = [1,2,2]`, the solution is:

```
[
[],
[1],
[1,2],
[1,2,2],
[2],
[2, 2]
]

```

```cpp
void findTheSubset(vector<int> A, vector<vector<int>> &ans, vector<int> a, int i){
    // Base Case
    if(i == A.size()){
        ans.push_back(a);
        return;
    }
    // Recursive Case 
    a.push_back(A[i]);
    findTheSubset(A, ans, a, i + 1);
    a.pop_back();   
    while(i + 1 < A.size() and A[i] == A[i+1]){
        i++;
    }
    findTheSubset(A, ans, a, i + 1);    
}

vector<vector<int> > Solution::subsetsWithDup(vector<int> &A) {
    vector<vector<int>> ans;
    vector<int> a;
    sort(A.begin(), A.end());
    findTheSubset(A, ans, a, 0);
    sort(ans.begin(), ans.end());
    return ans;
}
```