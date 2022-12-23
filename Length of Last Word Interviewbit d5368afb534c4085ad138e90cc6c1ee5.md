# Length of Last Word | Interviewbit

Created: May 16, 2022 5:29 PM
URL: https://www.interviewbit.com/problems/length-of-last-word/

**Problem Description**

Given a string **s** consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.

If the last word does not exist, return **0**.

Note: A word is defined as a character sequence consists of non-space characters only.

**Example:**

```
Given s = "Hello World",

return 5 as length("World") = 5.

```

Please make sure you try to solve this problem without using library functions. Make sure you only traverse the string once.

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```python
int Solution::lengthOfLastWord(const string &A) {
    int i = A.length() - 1;
    while(i >= 0 && A[i] == ' '){
        i--;
    }
    int res = 0;
    while(i >= 0){
        if(A[i] == ' '){
            return res;
        }
        res++;
        i--;
    }
    return res;
```