# Longest valid Parentheses | Interviewbit

Created: August 9, 2022 12:53 AM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/longest-valid-parentheses/

Given a string **A** containing just the characters **’(‘** and **’)’**.

Find the length of the **longest** valid (well-formed) parentheses substring.

**Input Format:**

```
The only argument given is string A.

```

**Output Format:**

```
Return the length of the longest valid (well-formed) parentheses substring.

```

**Constraints:**

```
1 <= length(A) <= 750000

```

**For Example**

```
Input 1:
    A = "(()"
Output 1:
    2
    Explanation 1:
        The longest valid parentheses substring is "()", which has length = 2.

Input 2:
    A = ")()())"
Output 2:
    4
    Explanation 2:
        The longest valid parentheses substring is "()()", which has length = 4.

```

```cpp
int Solution::longestValidParentheses(string A) {
    int ans = 0;
    stack<int> s;
    s.push(-1);
    
    for(int i = 0; i<A.size(); i++){
        if(A[i] == '('){
            s.push(i);
        }
        else{
            s.pop();
            if(s.empty()){
                s.push(i);
            }
            else{
                int len = i - s.top();
                ans = max(ans, len);
            }
        }
    }
    return ans;
}
```

```cpp
int Solution::longestValidParentheses(string A) {
    int n = A.length();
    if (n <= 1) {
        return 0;
    }
    int ret = 0, i = 0, j = 0;
    std::vector<int> table(n+1,0);
    for (i = 1; i <= n; ++i) {
        j = i - 2 - table[i-1];
        if (A[i-1] == '(' || j < 0 || A[j] == ')') {
            table[i] = 0;
        } else {
            table[i] = table[i-1]+2+table[j];
            ret = max(ret, table[i]);
        }
    }
    return ret;
}
```