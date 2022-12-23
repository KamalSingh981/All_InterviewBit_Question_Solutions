# NEXTGREATER | Interviewbit

Created: June 20, 2022 2:52 AM
Tags: Stacks
URL: https://www.interviewbit.com/problems/nextgreater/

Given an array, find the next greater element G[i] for every element A[i] in the array. The Next greater Element for an element A[i] is the first greater element on the right side of A[i] in array. 
 More formally,

```
G[i] for an element A[i] = an element A[j] such that
    j is minimum possible AND
    j > i AND
    A[j] > A[i]

```

Elements for which no greater element exist, consider next greater element as -1.

**Example:**

Input : `A : [4, 5, 2, 10]`

**Example 2:**

Input : `A : [3, 2, 1]`
 Output : `[-1, -1, -1]`

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
vector<int> Solution::nextGreater(vector<int> &A) {
    stack<int> s;
    vector<int> ans(A.size(),-1);
    s.push(A[A.size()-1]);
    for(int i = A.size()-2; i>=0; i--){
        if(A[i]<s.top()){
            ans[i] = s.top();
        }
        else{
            while(!s.empty() && A[i]>=s.top()){
                s.pop();
            }
            if(!s.empty()){
                ans[i] = s.top();
            }
        }
        s.push(A[i]);
    }
    return ans;
}
```