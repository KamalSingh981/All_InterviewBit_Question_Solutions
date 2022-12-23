# Merge K sorted arrays! | Interviewbit

Created: July 18, 2022 12:55 PM
Tags: Heap
URL: https://www.interviewbit.com/problems/merge-k-sorted-arrays/

**Problem Description**

You are given **K** sorted integer arrays in a form of 2D integer matrix **A** of size `K X N`.

You need to merge them into a single array and return it.

**Problem Constraints**

1 <= K, N <= 103

0 <= A[i][j] <= 108

A[i][j] <= A[i][j+1]

**Input Format**

First and only argument is an 2D integer matrix **A**.

**Output Format**

Return a integer array denoting the merged array you get after merging all the arrays in **A**.

**Example Input**

Input 1:

```
 A = [  [1, 2, 3]
        [2, 4, 6]
        [0, 9, 10]
     ]

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 You need to merge [1, 2, 3] , [2, 4, 6] and [0, 9, 10]  into a single array
 so the merged array will look like [0, 1, 2, 2, 3, 4, 6, 9, 10]

```

```cpp
typedef pair<int, pair<int, int>> node;

vector<int> Solution::solve(vector<vector<int> > &A) {
    
    priority_queue<node, vector<node>, greater<node>> pq;
    
    vector<int> ans;
    
    for(int i = 0; i<A.size(); i++){
        pq.push({A[i][0], {i , 0}});
    }
    
    while(!pq.empty()){
        node current_element = pq.top();
        pq.pop();
        
        int data = current_element.first;
        int row = current_element.second.first;
        int col = current_element.second.second;
        ans.push_back(data);
        
        
        if(col + 1 < A[row].size()){
            pq.push({A[row][col +1], {row, col +1}});
        }
    }   
    return ans;  
}
```