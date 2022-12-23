# Reverse String | Interviewbit

Created: June 19, 2022 3:47 PM
Tags: Stacks
URL: https://www.interviewbit.com/problems/reverse-string/

Given a string S, reverse the string using stack.

**Example :**

```
Input : "abc"
Return "cba"

```

PROBLEM APPROACH :

Complete solution in hints.

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
string Solution::reverseString(string A) {
    stack<char> s;
    for(int i = 0; i<A.length(); i++){
        s.push(A[i]);
    }
    A = "";
    while(!s.empty()){
        A += s.top();
        s.pop();
    }
    return A;  
}
```