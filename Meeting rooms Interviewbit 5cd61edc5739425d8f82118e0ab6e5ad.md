# Meeting rooms | Interviewbit

Created: July 25, 2022 11:55 PM
Tags: GreedyAlgorithm
URL: https://www.interviewbit.com/problems/meeting-rooms/

**Problem Description**

Given an 2D integer array **A** of size `N x 2` denoting time intervals of different meetings.

Where:

- **A[i][0]** = start time of the i meeting.
    
    th
    
- **A[i][1]** = end time of the i meeting.
    
    th
    

Find the **minimum number of conference rooms** required so that all meetings can be done.

**Problem Constraints**

1 <= N <= 10

0 <= A[i][0] < A[i][1] <= 2 * 109

**Input Format**

The only argument given is the matrix **A**.

**Output Format**

Return the minimum number of conference rooms required so that all meetings can be done.

**Example Input**

Input 1:

```
 A = [      [0, 30]
            [5, 10]
            [15, 20]
     ]

```

Input 2:

```
 A =  [     [1, 18]
            [18, 23]
            [15, 29]
            [4, 15]
            [2, 11]
            [5, 13]
      ]

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 Meeting one can be done in conference room 1 form 0 - 30.
 Meeting two can be done in conference room 2 form 5 - 10.
 Meeting three can be done in conference room 2 form 15 - 20 as it is free in this interval.

```

Explanation 2:

```
 Meeting one can be done in conference room 1 from 1 - 18.
 Meeting five can be done in conference room 2 from 2 - 11.
 Meeting four can be done in conference room 3 from 4 - 15.
 Meeting six can be done in conference room 4 from 5 - 13.
 Meeting three can be done in conference room 2 from 15 - 29 as it is free in this interval.
 Meeting two can be done in conference room 4 from 18 - 23 as it is free in this interval.

```

Priority Queue Solution 

```cpp
int Solution::solve(vector<vector<int> > &A) {
    sort(A.begin(), A.end());
    
    priority_queue<int, vector<int>, greater<int>> p;  
    int ans = 1;
    int maxi = 1;
    int fin = A[0][1];
    p.push(A[0][1]);
    for(int  i = 1; i< A.size(); i++){
        if(fin > A[i][0]){
            p.push(A[i][1]);
            fin = p.top();
            ans++;
        }
        else{
            p.pop();
            p.push(A[i][1]);
            fin = p.top();
        }
    }
    return ans;
}
```