# Subarray with B odd numbers | Interviewbit

Created: July 16, 2022 12:35 PM
Tags: Hashing
URL: https://www.interviewbit.com/problems/subarray-with-b-odd-numbers/

**Problem Description**

Given an array of integers **A** and an integer **B**.

Find the total number of subarrays having exactly B odd numbers.

**Problem Constraints**

1 <= length of the array <= 105

1 <= A[i] <= 109

0 <= B <= A

**Input Format**

The first argument given is the integer array A.
 The second argument given is integer B.

**Output Format**

Return the total number of subarrays having exactly B odd numbers.

**Example Input**

Input 1:

```
 A = [4, 3, 2, 3, 4]
 B = 2
```

Input 2:

```
 A = [5, 6, 7, 8, 9]
 B = 3
```

**Example Output**

**Example Explanation**

Explanation 1:

```
 The subarrays having exactly B odd numbers are:
 [4, 3, 2, 3], [4, 3, 2, 3, 4], [3, 2, 3], [3, 2, 3, 4]
```

Explanation 2:

```
 The subarrays having exactly B odd numbers is [5, 6, 7, 8, 9]
```

```cpp
int Solution::solve(vector<int> &A, int B) {
    int currsum = 0;
    int ans = 0;
    unordered_map<int, int> m;
    for(int i = 0; i<A.size(); i++){
        if(A[i]%2){
            currsum += 1;
        }
        if(currsum == B){
            ans++;
        }
        if(m.find(currsum-B) != m.end()){
            ans += m[currsum-B];
        }
        m[currsum]++;
    }
    return ans;
}
```