# Largest Rectangle in Histogram | Interviewbit

Created: June 20, 2022 2:00 PM
Tags: Stacks
URL: https://www.interviewbit.com/problems/largest-rectangle-in-histogram/

**Problem Description**

Given an array of integers **A** .

A represents a histogram i.e A[i] denotes height of the ith histogram's bar. Width of each bar is 1.

Find the area of the largest rectangle formed by the histogram.

**Problem Constraints**

1 <= |A| <= 100000

1 <= A[i] <= 1000000000

**Input Format**

The only argument given is the integer array A.

**Output Format**

Return the area of largest rectangle in the histogram.

**Example Input**

**Example Output**

**Example Explanation**

```cpp
int Solution::largestRectangleArea(vector<int> &A) {
    stack<int> s;
    A.push_back(0);
    int n = A.size();
    s.push(0);
    int ans = 0;
    for(int i=1; i<A.size(); i++){
        int minbar = A[i-1];
        if(s.empty() || A[i]>=A[s.top()]){
            s.push(i);
        }
        else{
            int mins = A[i-1];
            while(!s.empty() and A[i]<A[s.top()]){
                s.pop();
                if(s.empty()){
                    ans = max(ans, mins*i);
                }
                else{
                    ans = max(ans, mins*(i-s.top()-1));
                    mins = min(A[s.top()], mins);
                }
            }
            s.push(i);
        }
    }
    return ans;
}
```

InterviewBit Code

```cpp
int Solution::largestRectangleArea(vector<int> &A) {
    stack<int> st;
    int res = 0;
    A.push_back(0);
    int n = A.size();
    
    for(int i = 0; i < n; i++){
        
        while(!st.empty() && A[st.top()] >= A[i]){
            
            int tp = st.top();
            st.pop();
            int curr = A[tp] * (st.empty() ? i : (i - st.top() - 1));
            res = max(res, curr);
        }
        
        st.push(i);
    }
    return res;
}
```