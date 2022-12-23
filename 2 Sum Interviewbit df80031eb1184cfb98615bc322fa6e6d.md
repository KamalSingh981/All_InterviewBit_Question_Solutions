# 2 Sum | Interviewbit

Created: July 15, 2022 4:18 PM
Tags: Hashing
URL: https://www.interviewbit.com/problems/2-sum/

**Problem Description**

Given an array of integers, find two numbers such that they add up to a specific target number.

The function **twoSum** should return indices of the two numbers such that they add up to the target, where **index1** < **index2**. Please note that your returned answers (both **index1** and **index2** ) are not zero-based. Put both these numbers in order in an array and return the array from your function ( Looking at the function signature will make things clearer ). Note that, if no pair exists, return empty list.

If multiple solutions exist, output the one where **index2** is minimum. If there are multiple solutions with the minimum **index2**, choose the one with minimum **index1** out of them. 
`Input: [2, 7, 11, 15], target=9
Output: index1 = 1, index2 = 2`

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
vector<int> Solution::twoSum(const vector<int> &A, int B) {
    unordered_map<int, int> m;
    for(int i = 0; i<A.size(); i++){
        int q = B - A[i];
        if(m.find(A[i]) != m.end()){
            return {m[A[i]]+1, i+1};
        }
        else{
            if(m.find(q) == m.end()) {
                m[q] = i;
            }
        }
    }
    return {};
}
```