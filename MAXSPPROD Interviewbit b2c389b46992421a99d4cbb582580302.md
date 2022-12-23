# MAXSPPROD | Interviewbit

Created: June 20, 2022 2:38 PM
Tags: Stacks
URL: https://www.interviewbit.com/problems/maxspprod/

**Problem Description**

You are given an array **A** containing **N** integers. The special product of each **ith** integer in this array is defined as the product of the following:

1. **LeftSpecialValue:** For an index **i**, it is defined as the index **j** such that **A[j]>A[i]** and **(i>j)**. If multiple **A[j]'s** are present in multiple positions, the LeftSpecialValue is the maximum value of **j**.
2. **RightSpecialValue:** For an index **i**, it is defined as the index **j** such that **A[j]>A[i]** and **(j>i)**. If multiple **A[j]'s** are present in multiple positions, the RightSpecialValue is the minimum value of **j**.

Write a program to find the maximum special product of any integer in the array.

**NOTE:**  As the answer can be large, output your answer modulo 109 + 7.

**Problem Constraints**

1 <= N <= 105
 1 <= A[i] <= 109

**Input Format**

First and only argument is an integer array A.

**Output Format**

Return an integer denoting the maximum special product of any integer.

**Example Input**

Input 1:

```
 A = [1, 4, 3, 4]
```

Input 2:

```
 A = [10, 7, 100]
```

**Example Output**

**Example Explanation**

Explanation 1:

```
 For A[2] = 3, LeftSpecialValue is 1 and RightSpecialValue is 3.
 So, the ans is 1*3 = 3.

```

Explanation 2:

```
 There is not any integer having maximum special product > 0. So, the ans is 0.
```

```cpp
vector<int> smaller(vector<int> A){
    stack<int> s;
    s.push(0);
    vector<int> ans(A.size(), 0);
    for(int i = 1; i<A.size(); i++){
        if(A[s.top()]>A[i]){
            ans[i] = s.top();
        }
        else{
            while(!s.empty() && A[s.top()]<=A[i]){
                s.pop();
            }
            if(!s.empty()){
                ans[i] = s.top();
            }
        }
        s.push(i);
    }
    return ans;
}
vector<int> greaters(vector<int> A){
    stack<int> s;
    vector<int> ans(A.size(),0);
    s.push(A.size()-1);
    for(int i = A.size()-2; i>=0; i--){
        if(A[i]<A[s.top()]){
            ans[i] = s.top();
        }
        else{
            while(!s.empty() && A[i]>=A[s.top()]){
                s.pop();
            }
            if(!s.empty()){
                ans[i] = s.top();
            }
        }
        s.push(i);
    }
    return ans;
}

int Solution::maxSpecialProduct(vector<int> &A) {
    vector<int> sm = smaller(A);
    vector<int> gre = greaters(A);
    long long ans = 0;
    for(int i = 0; i<A.size(); i++){
        ans = max(ans, (long long)sm[i]*gre[i]);
    }
    return ans%1000000007;
}
```