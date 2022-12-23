# Combination Sum | Interviewbit

Created: July 12, 2022 8:03 PM
Tags: Backtracking, Recursion
URL: https://www.interviewbit.com/problems/combination-sum/

**Problem Description**

Given an array of candidate numbers **A** and a target number **B**, find all unique combinations in A where the candidate numbers sums to B.

The same repeated number may be chosen from A unlimited number of times.

**Note**:

1) All numbers (including target) will be positive integers.

2) Elements in a combination (a1, a2, … , ak) must be in non-descending order. (ie, a1 ≤ a2 ≤ … ≤ ak).

3) The combinations themselves must be sorted in ascending order.

4) CombinationA > CombinationB iff (a1 > b1) OR (a1 = b1 AND a2 > b2) OR ... (a1 = b1 AND a2 = b2 AND ... ai = bi AND ai+1 > bi+1)

5) The solution set must not contain duplicate combinations.

**Problem Constraints**

1 <= |A| <= 20

1 <= A[i] <= 50

1 <= B <= 500

**Input Format**

The first argument is an integer array A.

The second argument is integer B.

**Output Format**

Return a vector of all combinations that sum up to B.

**Example Input**

Input 1:

```
A = [2, 3]
B = 2

```

Input 2:

```
A = [2, 3, 6, 7]
B = 7

```

**Example Output**

Output 1:

```
[ [2] ]

```

Output 2:

```
[ [2, 2, 3] , [7] ]

```

**Example Explanation**

Explanation 1:

```
All possible combinations are listed.

```

Explanation 2:

```
All possible combinations are listed.

```

```cpp
void findCombinationSum(int ind, vector<int> A,int B,  vector<vector<int>> &ans,vector<int> a){
    if(ind == A.size()){
        if(B == 0){
            ans.push_back(a);
        }
        return;
    }

    if(A[ind] <= B){
        a.push_back(A[ind]);
        findCombinationSum(ind, A, B - A[ind], ans, a);
        a.pop_back();
    }
    findCombinationSum(ind + 1, A, B, ans, a);
}
vector<vector<int> > Solution::combinationSum(vector<int> &A, int B) {
    
    vector<vector<int>> ans;
    vector<int> a;
    vector<int> inde(100, 0);
    for(int i = 0; i<A.size(); i++){
        inde[A[i]]++;
    }
    A.clear();
    for(int i = 0; i<inde.size(); i++){
        if(inde[i] != 0){
            A.push_back(i);
        }
    }
    findCombinationSum(0, A, B, ans, a);
    return ans;
}
```