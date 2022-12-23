# Balanced Parantheses! | Interviewbit

Created: June 19, 2022 1:01 AM
Tags: Stacks
URL: https://www.interviewbit.com/problems/balanced-parantheses/

**Problem Description**

Given a string **A** consisting only of **'('** and **')'**.

You need to find whether parantheses in **A** is balanced or not ,if it is balanced then return **1** else return **0**.

**Problem Constraints**

**Input Format**

First argument is an string **A**.

**Output Format**

Return **1** if parantheses in string are balanced else return **0**.

**Example Input**

Input 1:

```
 A = "(()())"

```

Input 2:

```
 A = "(()"

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 Given string is balanced so we return 1

```

Explanation 2:

```
 Given string is not balanced so we return 0

```

```cpp
int Solution::solve(string A) {
    stack<char> s;
    for(int i =0; i<A.length(); i++){
        if(A[i] == '('){
            s.push(A[i]);
        }
        else{
            if(s.empty() or s.top() != '('){
                return 0;
            }
            s.pop();
        }
    }
    return s.empty();
}
```