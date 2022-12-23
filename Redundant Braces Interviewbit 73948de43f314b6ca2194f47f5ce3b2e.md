# Redundant Braces | Interviewbit

Created: June 19, 2022 4:20 PM
Tags: Stacks
URL: https://www.interviewbit.com/problems/redundant-braces/

**Problem Description**

Given a string **A** denoting an expression. It contains the following operators `'+', '-', '*', '/'`.

Chech whether A has redundant braces or not.

**NOTE:** A will be always a valid expression.

**Problem Constraints**

**Input Format**

The only argument given is string A.

**Output Format**

Return 1 if A has redundant braces, else return 0.

**Example Input**

Input 1:

```
 A = "((a+b))"
```

Input 2:

```
 A = "(a+(a+b))"
```

**Example Output**

**Example Explanation**

Explanation 1:

```
 ((a+b)) has redundant braces so answer will be 1.
```

Explanation 2:

```
 (a+(a+b)) doesn't have have any redundant braces so answer will be 0.
```

```cpp
int Solution::braces(string A) {
    stack<char> s;
    for(int i=0; i<A.length(); i++){
        if(A[i] == ')' and s.top() == '(') return 1;
        else if(A[i] == ')'){
            int count = 0;
            while(!s.empty() && s.top() != '('){
                s.pop();
                count++;
            }
            s.pop();
            if(count<=1){
                return 1;
            }
        }
        else{
            s.push(A[i]);
        }
    }
    return 0;
}
```