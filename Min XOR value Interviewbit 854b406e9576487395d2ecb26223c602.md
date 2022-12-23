# Min XOR value | Interviewbit

Created: June 15, 2022 6:33 PM
Tags: bit manipullation
URL: https://www.interviewbit.com/problems/min-xor-value/

Given an integer array **A** of **N** integers, find the pair of integers in the array which have minimum `XOR` value. Report the minimum `XOR` value.

**Input Format:**

```
    First and only argument of input contains an integer array A

```

**Output Format:**

```
    return a single integer denoting minimum xor value

```

**Constraints:**

```
2 <= N <= 100 000
0 <= A[i] <= 1 000 000 000

```

**For Examples :**

```
Example Input 1:
    A = [0, 2, 5, 7]
Example Output 1:
    2
Explanation:
    0 xor 2 = 2
Example Input 2:
    A = [0, 4, 7, 9]
Example Output 2:
    3

```

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```python
int Solution::findMinXor(vector<int> &A) {
    int ans = INT_MAX;
    sort(A.begin(), A.end());
    for(int i = 0; i<A.size()-1; i++){        
        ans = min(ans, A[i]^A[i+1]);        
    }
    return ans;
}
```