# Profit Maximisation | Interviewbit

Created: July 18, 2022 4:25 PM
Tags: Heap
URL: https://www.interviewbit.com/problems/profit-maximisation/

**Problem Description**

Given an array **A** , representing seats in each row of a stadium. You need to sell tickets to **B** people.

Each seat costs equal to the number of vacant seats in the row it belongs to. The task is to maximize the profit by selling the tickets to B people.

**Problem Constraints**

**Input Format**

First argument is the array A.

Second argument is integer B.

**Output Format**

Return one integer, the answer to the problem.

**Example Input**

Input 1:

```
A = [2, 3]
B = 3

```

Input 2:

```
A = [1, 4]
B = 2

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 First you serve the seat with number = 3. Then with 2 and then with 2. hence answer = 3 + 2 + 2 = 7.

```

Explanation 2:

```
 You give both tickets from the row with 4 seats. 4 + 3 = 7.

```

```cpp
int Solution::solve(vector<int> &A, int B) {  
    int ans = 0;
    priority_queue<int> pq;
    for(int i = 0; i<A.size(); i++){
        pq.push(A[i]);
    }
    
    for(int i = 0; i<B; i++){
        int t = pq.top();
        ans += t;   
        pq.pop();
        pq.push(t-1);
    }
    return ans;
}
```