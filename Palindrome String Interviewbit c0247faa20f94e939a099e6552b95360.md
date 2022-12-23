# Palindrome String | Interviewbit

Created: May 16, 2022 11:36 PM
URL: https://www.interviewbit.com/problems/palindrome-string/

Given a string, determine if it is a palindrome, considering only alphanumeric characters and ignoring cases.

**Example:**

`"A man, a plan, a canal: Panama"` is a palindrome.

`"race a car"` is not a palindrome.

Return `0 / 1` ( 0 for false, 1 for true ) for this problem

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```python
int Solution::isPalindrome(string A) {
    int i = 0, j = (int)A.size() - 1;
    while(i < j)
    {
        while(i < j && !isalnum(A[i])) i++;
        while(i < j && !isalnum(A[j])) j--;
        if (toupper(A[i]) != toupper(A[j])) return false; 
        i++;
        j--;
    }
    return true;
}
```