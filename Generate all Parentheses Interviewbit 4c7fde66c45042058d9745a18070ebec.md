# Generate all Parentheses | Interviewbit

Created: June 19, 2022 3:42 PM
Tags: Stacks
URL: https://www.interviewbit.com/problems/generate-all-parentheses/

Given a string containing just the characters `'(', ')', '{', '}', '[' and ']'`, determine if the input string is valid.

The brackets must close in the correct order, `"()"` and `"()[]{}"` are all valid but `"(]"` and `"([)]"` are not.

Return `0 / 1` ( 0 for false, 1 for true ) for this problem

PROBLEM APPROACH :

Complete solution in hints.

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
int Solution::isValid(string A) {
    stack<char> s;
    for(int i = 0; i<A.length(); i++){
        char ch = (char)A[i];
        if(s.empty() && (ch == '}' || ch == ']' || ch== ')' )){
            return 0;
        }
        else if(!s.empty() && ((s.top() == '(' && ch == ')') || (s.top() == '[' && ch == ']')  || (s.top() == '{' && ch == '}'))){
            s.pop();
        }
        else{
            s.push(ch);
        }
    }
    return  s.empty();
}
```