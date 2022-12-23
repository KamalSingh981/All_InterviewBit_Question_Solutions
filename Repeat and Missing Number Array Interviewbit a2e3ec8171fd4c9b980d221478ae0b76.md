# Repeat and Missing Number Array | Interviewbit

Created: May 15, 2022 3:49 PM
URL: https://www.interviewbit.com/problems/repeat-and-missing-number-array/

There are certain problems which are asked in the interview to also check how you take care of **overflows** in your problem.
 This is one of those problems.
 Please take extra care to make sure that you are type-casting your ints to long properly and at all places. **Try to verify if your solution works if number of elements is as large as 105**

> 
> 
> 
> **Food for thought** :
> 
> - Even though it might not be required in this problem, in some cases, you might be required to order the operations cleverly so that the numbers do not overflow.  For example, if you need to calculate n! / k! where n! is factorial(n), one approach is to calculate factorial(n), factorial(k) and then divide them.  Another approach is to only multiple numbers from `k + 1 ... n` to calculate the result.  Obviously approach 1 is more susceptible to overflows.

You are given a read only array of n integers from 1 to n.

Each integer appears exactly once except A which appears twice and B which is missing.

Return A and B.

*Note: Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?*

*Note that in your output A should precede B.*

**Example:**

```
Input:[3 1 2 5 3]

Output:[3, 4]

A = 3, B = 4

```

### Using O(n) space

```cpp
vector<int> Solution::repeatedNumber(const vector<int> &A) {
    int d = A.size();
    int arr[d] = {0};
    for(int i = 0; i<d; i++){
        arr[A[i]-1]++;
    }
    int first;
    int second;
    for(int i=0; i<d; i++){
        if(arr[i]==2){
            first = i+1;
        }
        else if(arr[i]==0){
            second = i+1;
        }
    }
    vector<int> q;
    q.push_back(first);
    q.push_back(second);
    return q;
}
```

### Without using space

```cpp
vector<int> Solution::repeatedNumber(const vector<int> &A) {
    vector<int> ret(2);
    long long sumOfA = 0, sumOfA2 = 0;
    long long temp;
    int retA, retB;
    int n = A.size();
    for (int i = 0; i < n; i++) {
        temp = A[i];
        sumOfA += temp;
        sumOfA2 += temp*temp;
        temp = i + 1;
        sumOfA -= temp;
        sumOfA2 -= temp*temp;
    }
    sumOfA2 = sumOfA2/sumOfA;
    retA = (int)((sumOfA + sumOfA2)/2);
    retB = (int)(sumOfA2-retA);
    ret[0] = retA;
    ret[1] = retB;
    return ret;
}
```