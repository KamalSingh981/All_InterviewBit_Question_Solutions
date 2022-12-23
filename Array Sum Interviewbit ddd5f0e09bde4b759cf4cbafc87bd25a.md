# Array Sum | Interviewbit

Created: May 9, 2022 1:49 AM
URL: https://www.interviewbit.com/problems/array-sum/

**Problem Description**

You are given two numbers represented as integer arrays **A** and **B**, where each digit is an element.
 You have to return an array which representing the sum of the two given numbers.

The last element denotes the least significant bit, and the first element denotes the most significant bit.

**Problem Constraints**

**Input Format**

The first argument is an integer array A. The second argument is an integer array B.

**Output Format**

**Example Input**

Input 1:

```
A = [1, 2, 3]
B = [2, 5, 5]

```

Input 2:

```
A = [9, 9, 1]
B = [1, 2, 1]

```

**Example Output**

Output 1:

```
[3, 7, 8]

```

Output 2:

```
[1, 1, 1, 2]

```

**Example Explanation**

Explanation 1:

```
Simply, add all the digits in their place.
```

Explanation 2:

```
991 + 121 = 1112
Note that the resultant array size might be larger.

```

```cpp
#include<iostream>
#include<algorithm>
#include <bits/stdc++.h>
using namespace std;
vector<int> Solution::addArrays(vector<int> &A, vector<int> &B) {
    reverse(A.begin(), A.end());
    reverse(B.begin(), B.end());
    int a = A.size();
    int b = B.size();
    int carry = 0;
    vector<int> ans;
    int digits = max(a, b);

    for(int i=0; i<digits; i++){
        int sum = 0;
        if (i>=a){
            sum = B[i] + carry;
        }
        else if (i>=b){
            sum = A[i] + carry;
        }
        else{
            sum = A[i] + B[i] + carry;
        }
        
        ans.push_back(sum%10);
        carry = sum/10;
    }
    if(carry!=0){
        ans.push_back(carry);
    }
    reverse(ans.begin(), ans.end());
    return ans;
}
```