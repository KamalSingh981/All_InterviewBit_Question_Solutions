# Longest Substring Without Repeat | Interviewbit

Created: July 17, 2022 1:39 AM
Tags: Hashing
URL: https://www.interviewbit.com/problems/longest-substring-without-repeat/

Given a string, 
 find the length of the longest substring without repeating characters.

**Example:**

The longest substring without repeating letters for `"abcabcbb"` is `"abc"`, which the length is `3`.

For `"bbbbb"` the longest substring is `"b"`, with the length of `1`.

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
int Solution::lengthOfLongestSubstring(string A){
    unordered_map<char, int> m;
    int l = 0, ans = 1;
    int n = A.length();
    for(int i = 0; i<n; i++){
        if(m.find(A[i]) != m.end() and m[A[i]]>=l){
            ans = max(ans, i -l);
            l = m[A[i]]+1;
        }
        
        m[A[i]] = i;
    }   
    
    ans = max(ans, n-l);
    return ans;
}
```