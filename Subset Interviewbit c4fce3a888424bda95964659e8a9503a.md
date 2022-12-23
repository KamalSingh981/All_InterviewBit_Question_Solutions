# Subset | Interviewbit

Created: July 12, 2022 11:56 AM
Tags: Backtracking, Recursion
URL: https://www.interviewbit.com/problems/subset/

Given a set of distinct integers, S, return all possible subsets.

> 
> 
> 
> **Note:**
> 
> - Elements in a subset must be in non-descending order.
> - The solution set must not contain duplicate subsets.
> - Also, the subsets should be sorted in ascending ( lexicographic ) order.
> - The list is not necessarily sorted.

**Example :**

If `S = [1,2,3]`, a solution is:

```cpp
void recursive(vector<int> &A, int e, vector<vector<int> > &a, vector<int> &a1){
    a.push_back(a1);
    for(int i = e; i<A.size(); i++){
        a1.push_back(A[i]);
        recursive(A, i+1, a, a1);
        a1.pop_back();
    }
}

vector<vector<int> > Solution::subsets(vector<int> &A) {
    vector<vector<int>> ans;
    vector<int> a;
    sort(A.begin(), A.end());
    recursive(A, 0, ans, a);
    return ans;
}
```

```cpp
void findCombinationSum(vector<int> &A, int  B, vector<vector<int>> &a, vector<int> a1, int Sum)
{
    // Base Case
    if(Sum == B){
        a.push_back(a1);
        return;
    }
    else if(Sum > B){
        return;
    }
    for(int i=0; i<A.size(); i++){
        a1.push_back(A[i]);
        findCombinationSum(A, B, a, a1, Sum + A[i]);
    }
    
    
}
```