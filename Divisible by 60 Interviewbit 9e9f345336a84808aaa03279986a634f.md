# Divisible by 60 | Interviewbit

Created: May 11, 2022 1:15 AM
URL: https://www.interviewbit.com/problems/divisible-by-60/

**Problem Description**

Given a large number represent in the form of an integer array **A**, where each element is a digit.

You have to find whether there exists any permutation of the array **A** such that the number becomes divisible by 60.

Return 1 if it exists, 0 otherwise.

**Problem Constraints**

**Input Format**

**Output Format**

**Example Input**

Input 1:

```
A = [0, 6]

```

Input 2:

```
A = [2, 3]

```

**Example Output**

Output 1:

```
1

```

Output 2:

```
0

```

**Example Explanation**

Explanation 1:

```
We can rearrange the digits to form 60, which is divisible by 60.
```

Explanation 2:

```
There are only two possible permutations: [23, 32].
Both of them are not divisible by 60.

```

```python
int Solution::divisibleBy60(vector<int> &A) {
    int n = A.size();
    if(n == 1 && A[0] == 0) return 1;
    if(n < 2) return 0;
    if(n == 2) {
        sort(A.begin(), A.end());
        if(A[1] < 6) return 0;
    }
    int checkFor10 = -1;
    for(int i = 0; i < n; i++) {
        if(A[i] == 0) {
            checkFor10 = 1;
            break;
        }
    }
    
    int checkFor2 = -1;
    for(int i = 0; i < n; i++) {
        if(A[i]%2 == 0) {
            checkFor2 = 1;
            break;
        }
    }
    

    int checkFor3 = -1;
    int sum = 0;
    for(int i = 0; i < n; i++) {
        sum += A[i];
    }
    if(sum%3 == 0) {
        checkFor3 = 1;
    } 
    if(checkFor3 == 1 && checkFor2 == 1 && checkFor10 == 1) return 1;

    return 0;
}
```