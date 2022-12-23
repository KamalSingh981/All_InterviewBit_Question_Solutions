# Min Stack | Interviewbit

Created: June 19, 2022 5:24 PM
Tags: Stacks
URL: https://www.interviewbit.com/problems/min-stack/

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

> 
> 
> - **push(x)** – Push element x onto stack.
> - **pop()** – Removes the element on top of the stack.
> - **top()** – Get the top element.
> - **getMin()** – Retrieve the minimum element in the stack.

Note that all the operations have to be constant time operations.

Questions to ask the interviewer :

```
Q: What should getMin() do on empty stack?
A: In this case, return -1.

Q: What should pop do on empty stack?
A: In this case, nothing.

Q: What should top() do on empty stack?
A: In this case, return -1

```

> 
> 
> 
> **NOTE** : If you are using your own declared global variables, make sure to clear them out in the constructor.
> 

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

With using only one stack

```cpp
stack<int> s;
int mins;
MinStack::MinStack() {
    while(!s.empty()) s.pop();
}

void MinStack::push(int x) {
    if(s.empty()){
        mins = x;
        s.push(x);
    }
    else if(x<mins){
        s.push(2*x-mins);
        mins = x;
    }
    else s.push(x);
}

void MinStack::pop() {
    if(s.empty()){
        return;
    }
    if(s.top()<mins){
        int prev = 2*mins - s.top();
        mins = prev;
        s.pop();
    }
    else{
        s.pop();
    }
}

int MinStack::top() {
    if(s.empty()){
        return -1;
    }
    if(s.top()<mins) return mins;
    return s.top();
}

int MinStack::getMin() {
    if(s.empty()){
        return -1;
    }
    return mins;
}
```

Implementation using two stacks

```cpp
stack<int> s;
stack<int> min_vals;
MinStack::MinStack() {
    while(!s.empty()) s.pop();
    while(!min_vals.empty()){
        min_vals.pop();
    }
}

void MinStack::push(int x) {
    if(min_vals.empty() || x <= min_vals.top()){
        min_vals.push(x);
    }
    s.push(x);
}

void MinStack::pop() {
    if(s.empty()){
        return;
    }
    if(min_vals.top() == s.top()){
        min_vals.pop();
    }
    s.pop();
}

int MinStack::top() {
    if(s.empty()){
        return -1;
    }
    return s.top();
}

int MinStack::getMin() {
    if(min_vals.empty()){
        return -1;
    }
    return min_vals.top();
```