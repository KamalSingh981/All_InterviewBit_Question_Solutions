# Max Rectangle in Binary Matrix | Interviewbit

Created: August 4, 2022 11:20 PM
Tags: Stacks
URL: https://www.interviewbit.com/problems/max-rectangle-in-binary-matrix/

Given a 2D binary matrix filled with `0`’s and `1`’s, find the largest rectangle containing **all ones** and return its area.

Bonus if you can solve it in O(n^2) or less.

**Example :**

```
A : [  1 1 1
       0 1 1
       1 0 0
    ]

Output : 4

As the max area rectangle is created by the 2x2 rectangle created by (0,1), (0,2), (1,1) and (1,2)

```

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
int largestArea(vector<int> &A){
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

int Solution::maximalRectangle(vector<vector<int> > &A) {
    
    int ans = INT_MIN;
    
    for(int i = 0; i<A.size(); i++){
        for(int j = 0; j<A[0].size(); j++){
            if(i!=0){
                if(A[i][j] != 0)
                A[i][j] += A[i-1][j];
            }
        }
        ans = max(ans, largestArea(A[i]));
    }
    
    return ans; 
}
```