# First Repeating element | Interviewbit

Created: July 15, 2022 12:04 AM
Tags: Hashing
URL: https://www.interviewbit.com/problems/first-repeating-element/

**Problem Description**

Given an integer array **A** of size **N**, find the first repeating element in it.

We need to find the element that occurs **more than once** and whose index of first occurrence is **smallest**.

If there is no repeating element, return -1.

**Problem Constraints**

1 <= N <= 105

1 <= A[i] <= 109

**Input Format**

First and only argument is an integer array A of size N.

**Output Format**

Return an integer denoting the first repeating element.

**Example Input**

Input 1:

```
 A = [10, 5, 3, 4, 3, 5, 6]
```

Input 2:

```
 A = [6, 10, 5, 4, 9, 120]
```

**Example Output**

Output 1:

```
 5
```

Output 2:

```
 -1
```

**Example Explanation**

Explanation 1:

```
 5 is the first element that repeats
```

Explanation 2:

```
 There is no repeating element, output -1
```

```cpp
int Solution::solve(vector<int> &A) {
    unordered_map<int, pair<int ,int>> count;
    int ans = -1;
    for(int i=A.size()-1; i>=0; i--){
        count[A[i]].first = i;
        count[A[i]].second++;
    }
    int i = A.size();
    for(auto s:count){
        if(s.second.second>1 && s.second.first<i){
            i = s.second.first;
            ans = s.first;
        }
    }
    return ans;   
}
```

InterviewBit Code

```cpp
int Solution::solve(vector<int> &A) {
    int n = A.size();
    // Initialize index of first repeating element
    int mini = -1;

    // Creates an empty hashset named ump
    unordered_map<int,int> ump;

    // Traverse the input array from right to left
    for (int i = n - 1; i >= 0; i--)
    {
        // If element is already in hash set, update min
        if (ump.find(A[i]) != ump.end())
            mini = i;
        else   // Else add element to hash set
            ump[A[i]] = 1;
    }
    if(mini == -1){
        return mini;
    }
    return A[mini];
}
```