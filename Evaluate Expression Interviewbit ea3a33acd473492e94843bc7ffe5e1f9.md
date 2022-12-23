# Evaluate Expression | Interviewbit

Created: June 19, 2022 6:04 PM
Tags: Stacks
URL: https://www.interviewbit.com/problems/evaluate-expression/

**Problem Description**

An arithmetic expression is given by a charater array A of size N. Evaluate the value of an arithmetic expression in Reverse Polish Notation.

Valid operators are +, -, *, /. Each character may be an integer or an operator.

**Problem Constraints**

**Input Format**

The only argument given is character array A.

**Output Format**

Return the value of arithmetic expression formed using reverse Polish Notation.

**Example Input**

```
Input 1:
    A =   ["2", "1", "+", "3", ""]

```

```
Input 2:
    A = ["4", "13", "5", "/", "+"]

```

*Example OutputExample Explanation**

```
Explaination 1:
    starting from backside:
    * : () * ()
    3 : () * (3)
    + : (() + ()) * (3)
    1 : (() + (1)) * (3)
    2 : ((2) + (1)) * (3)
    ((2) + (1)) * (3) = 9

```

```
Explaination 2:
    + : () + ()
    / : () + (() / ())
    5 : () + (() / (5))
    13 : () + ((13) / (5))
    4 : (4) + ((13) / (5))
    (4) + ((13) / (5)) = 6

```

```cpp
#include <string>

int Solution::evalRPN(vector<string> &A) {
    stack<int> s;
    for(int i = 0; i<A.size(); i++){
        if(A[i] == "*"){
            int a = s.top();
            s.pop();
            int b = s.top();
            s.pop();
            s.push(a*b);
        }
        else if(A[i] == "-"){
            int a = s.top();
            s.pop();
            int b = s.top();
            s.pop();
            s.push(b-a);
        }
        else if(A[i] == "+"){
            int a = s.top();
            s.pop();
            int b = s.top();
            s.pop();
            s.push(a+b);
        }
        else if(A[i] == "/"){
            int a = s.top();
            s.pop();
            int b = s.top();
            s.pop();
            s.push(b/a);
        }
        
        else{
            s.push(stoi(A[i]));
        }
    }
    return s.top();
}
```