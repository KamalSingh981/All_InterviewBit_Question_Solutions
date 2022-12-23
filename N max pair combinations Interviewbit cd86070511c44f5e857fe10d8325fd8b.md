# N max pair combinations | Interviewbit

Created: July 18, 2022 6:15 PM
Tags: Heap
URL: https://www.interviewbit.com/problems/n-max-pair-combinations/

**Problem Description**

Given two integers arrays **A** and **B** of size **N** each.

Find the **maximum N elements** from the sum combinations (Ai + Bj) formed from elements in array A and B.

**Problem Constraints**

1 <= N <= 2 * 105

- 1000 <= A[i], B[i] <= 1000

**Input Format**

First argument is an integer array A.
 Second argument is an integer array B.

**Output Format**

Return an intger array denoting the N maximum element in descending order.

**Example Input**

Input 1:

```
 A = [1, 4, 2, 3]
 B = [2, 5, 1, 6]
```

Input 2:

```
 A = [2, 4, 1, 1]
 B = [-2, -3, 2, 4]
```

**Example Output**

Output 1:

```
 [10, 9, 9, 8]
```

Output 2:

```
 [8, 6, 6, 5]
```

**Example Explanation**

Explanation 1:

```
 4 maximum elements are 10(6+4), 9(6+3), 9(5+4), 8(6+2).
```

Explanation 2:

```
 4 maximum elements are 8(4+4), 6(4+2), 6(4+2), 5(4+1).
```

```cpp
vector<int> Solution::solve(vector<int> &A, vector<int> &B) {
    sort(A.begin(), A.end());
    sort(B.begin(), B.end());
    
    priority_queue<pair<int, pair<int, int>>> pq;
    
    set<pair<int, int>> s;
    
    int n = A.size();
    pq.push({A[n-1] + B[n-1], {n-1, n-1}});
    s.insert({n-1, n-1});
    
    vector<int> ans;
    
    for(int k = 0; k<n; k++){
        pair<int, pair<int, int>> ele = pq.top();
        pq.pop();
        
        ans.push_back(ele.first);
        
        int i = ele.second.first;
        int j = ele.second.second;
        
        if(i > 0 and s.count({i -1, j}) == 0){
            pq.push({A[i-1] + B[j], {i-1, j}});
            s.insert({ i -1, j});
        }
        if(j > 0 and s.count({i, j-1}) == 0){
            pq.push({A[i] + B[j -1 ], {i, j-1}});
            s.insert({ i, j - 1});
        }
    }
    return ans;  
}
```