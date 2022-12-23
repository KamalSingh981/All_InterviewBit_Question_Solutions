# Capacity To Ship Packages Within B Days | Interviewbit

Created: May 24, 2022 3:00 AM
Tags: Binary Search, Hard
URL: https://www.interviewbit.com/problems/capacity-to-ship-packages-within-b-days/

**Problem Description**

A conveyor belt has packages that must be shipped from one port to another within **B** days.

The ith package on the conveyor belt has a weight of **A[i]**. Each day, we load the ship with packages on the conveyor belt (in the order given by weights). We may not load more weight than the maximum weight capacity of the ship.

Return the least weight capacity of the ship that will result in all the packages on the conveyor belt being shipped within **B** days.

**Problem Constraints**

**Input Format**

First argument is array of integers A denoting the weights.

Second argument is the integer B denoting the number of days.

**Output Format**

**Example Input**

Input 1:

```
A = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
B = 5

```

Input 2:

```
A = [3, 2, 2, 4, 1, 4]
B = 3

```

**Example Output**

**Example Explanation**

Explanation 1:

```
A ship capacity of 15 is the minimum to ship all the packages in 5 days like this:
1st day: 1, 2, 3, 4, 5
2nd day: 6, 7
3rd day: 8
4th day: 9
5th day: 10
Note that the cargo must be shipped in the order given, so using a ship of capacity 14 and
splitting the packages into parts like (2, 3, 4, 5), (1, 6, 7), (8), (9), (10) is not allowed.
```

Explanation 2:

```
A ship capacity of 6 is the minimum to ship all the packages in 3 days like this:
1st day: 3, 2
2nd day: 2, 4
3rd day: 1, 4
```

```cpp
#include <bits/stdc++.h>

bool isvalid(vector<int> A, int n, int D, int mx){
    int st= 1;
    int sum = 0;

    for(int i=0; i<n; i++){
        sum += A[i];
        if(sum>mx){
            st++;
            sum  = A[i];
        }
        if(st>D){
            return false;
        }
    }
    return true;
}

int shipwithinDays(vector<int> A, int D, int n){
    int sum = 0;
    for(int i = 0; i<n; i++){
        sum += A[i];
    }
    int s = *max_element(A.begin(), A.end());

    int e = sum;
    int ans = -1;

    while (s <= e){
        int mid = s + (e - s)/2;
        if(isvalid(A, n, D, mid)){
            ans = mid;
            e = mid -1;
        }
        else {
            s = mid +1;
        }
    }
    return ans;
}
int Solution::solve(vector<int> &A, int B) {
    return shipwithinDays(A, B, A.size());
}
```