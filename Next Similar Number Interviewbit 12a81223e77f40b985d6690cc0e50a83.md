# Next Similar Number | Interviewbit

Created: May 18, 2022 12:30 AM
URL: https://www.interviewbit.com/problems/next-similar-number/

**Problem Description**

Given a number **A** in a form of string.

You have to find the smallest number that has same set of digits as A and is greater than A.

If A is the greatest possible number with its set of digits, then return -1.

**Problem Constraints**

1 <= A <= 10100000

A doesn't contain leading zeroes.

**Input Format**

First and only argument is an numeric string denoting the number **A**.

**Output Format**

Return a string denoting the smallest number greater than A with same set of digits , if A is the largest possible then return -1.

**Example Input**

Input 1:

```
 A = "218765"

```

Input 2:

```
 A = "4321"

```

**Example Output**

Output 1:

```
 "251678"

```

Output 2:

```
 "-1"

```

**Example Explanation**

Explanation 1:

```
 The smallest number greater then 218765 with same set of digits is 251678.

```

Explanation 2:

```
 The given number is the largest possible number with given set of digits so we will return -1.

```

```cpp
string Solution::solve(string A) {
    int n = A.length();
    int k,l;
    // cout<<A.length();
    if (A.length()==1) {
        // cout<<"hey";
        return "-1";
    }
    for (k  = n-2; k >=0; k--){
        if(A[k]<A[k+1]){
            break;
        }
    }
    if(k<0) return "-1";
    for( l = n-1; l >k; l--){
        if(A[l]>A[k]){
            break;
        }
    }
    swap(A[k], A[l]);
    std::reverse(A.begin()+k+1, A.end()); 
    return A;
}
```