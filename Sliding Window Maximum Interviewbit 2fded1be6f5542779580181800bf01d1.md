# Sliding Window Maximum | Interviewbit

Created: June 20, 2022 5:08 PM
Tags: Queue
URL: https://www.interviewbit.com/problems/sliding-window-maximum/

Given an array of integers **A**. There is a sliding window of size **B** which 
 is moving from the very left of the array to the very right. 
 You can only see the w numbers in the window. Each time the sliding window moves 
 rightwards by one position. You have to find the maximum for each window. 
 The following example will give you more clarity.

The array **A** is `[1 3 -1 -3 5 3 6 7]`, and **B** is 3.

**Window position**

**Max**

Return an array **C**, where **C[i]** is the maximum value of from **A[i]** to **A[i+B-1]**.

**Note**: If **B** > length of the array, return 1 element with the max of the array.

**Input Format**

```
The first argument given is the integer array A.
The second argument given is the integer B.

```

**Output Format**

```
Return an array C, where C[i] is the maximum value of from A[i] to A[i+B-1]

```

**For Example**

```
Input 1:
    A = [1, 3, -1, -3, 5, 3, 6, 7]
    B = 3
Output 1:
    C = [3, 3, 5, 5, 6, 7]

```

Brute force solution

```cpp
vector<int> Solution::slidingMaximum(const vector<int> &A, int B) {
    vector<int> ans;
    if(B==0){
        return ans;
    }
    if(A.size()==1){
        ans.push_back(A[0]);
        return ans;
    }
    for(int i=0; i<=A.size()-B; i++){
        int maxi = INT_MIN;
        for(int j = i; j<B+i; j++){
            maxi = max(maxi, A[j]);
        }
        ans.push_back(maxi);
    }
    
    return ans;
}
```

More Efficient Approach using doubly queue

```cpp
vector<int> Solution::slidingMaximum(const vector<int> &A, int B) {
    deque<int> dq;
    vector<int> ans;
    
    
    for(int i =0; i<B; i++){
        while(!dq.empty() && dq.back()<A[i]){
            dq.pop_back();
        }
        dq.push_back(A[i]);
    }
    ans.push_back(dq.front());
    for(int i = B; i<A.size(); i++){
        if(A[i-B] == dq.front()){
            dq.pop_front();
             
        }
         while(!dq.empty() && dq.back()<A[i]){
            dq.pop_back();
        }
        dq.push_back(A[i]);
        ans.push_back(dq.front());
    }
    return ans;
}
```