# Amazing Subarrays | Interviewbit

Created: May 16, 2022 11:57 PM
URL: https://www.interviewbit.com/problems/amazing-subarrays/

You are given a string **S**, and you have to find all the **amazing substrings** of **S**.

Amazing Substring is one that starts with a **vowel** (a, e, i, o, u, A, E, I, O, U).

**Input**

```
Only argument given is string S.

```

**Output**

```
Return a single integer X mod 10003, here X is number of Amazing Substrings in given string.

```

**Constraints**

```
1 <= length(S) <= 1e6
S can have special characters

```

**Example**

```
Input
    ABEC

Output
    6

Explanation
	Amazing substrings of given string are :
	1. A
	2. AB
	3. ABE
	4. ABEC
	5. E
	6. EC
	here number of substrings are 6 and 6 % 10003 = 6.

```

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```python
int Solution::solve(string A) {
    int d = A.length();
    int ans = 0;
    for(int i=0; i<d; i++){
        if (A[i] == 'a' or A[i] == 'e' or
        A[i] == 'i' or A[i] == 'o' or A[i] == 'u' or A[i] == 'A' or A[i] == 'E' or
        A[i] == 'I' or A[i] == 'O' or A[i] == 'U'){
            ans = (ans +d - i)%10003;
        }
    }
    return ans;
}
```