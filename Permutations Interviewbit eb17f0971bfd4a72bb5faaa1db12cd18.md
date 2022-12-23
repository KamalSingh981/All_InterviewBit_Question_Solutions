# Permutations | Interviewbit

Created: July 13, 2022 2:25 AM
Tags: Backtracking, Recursion
URL: https://www.interviewbit.com/problems/permutations/

Given a collection of numbers, return all possible permutations.

**Example:**

`[1,2,3]` will have the following permutations:

```
[1,2,3]
[1,3,2]
[2,1,3]
[2,3,1]
[3,1,2]
[3,2,1]

```

> 
> 
> 
> **NOTE**
> 
> - No two entries in the permutation sequence should be the same.
> - For the purpose of this problem, assume that all the numbers in the collection are unique.

> 
> 
> 
> **Warning :** DO NOT USE LIBRARY FUNCTION FOR GENERATING PERMUTATIONS. Example : next_permutations in C++ / itertools.permutations in python. *If you do, we will disqualify your submission retroactively and give you penalty points.*
> 

```cpp
void findAllPermutation(vector<int> &A, vector<vector<int>> &ans,int i){
    // Base Case
    if(i == A.size() -1){
        ans.push_back(A);
        return;
    }  
    // Recursive Case 
    for(int k = i; k<A.size(); k++){
        swap(A[k], A[i]); 
        findAllPermutation(A, ans, i + 1);
        swap(A[k], A[i]);
    }
}

vector<vector<int> > Solution::permute(vector<int> &A) {
    vector<vector<int>> ans;
    findAllPermutation(A, ans, 0);
    return ans;
     
}
```