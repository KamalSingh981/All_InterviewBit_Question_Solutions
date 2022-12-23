# Window String | Interviewbit

Created: July 17, 2022 12:59 AM
Tags: Hashing
URL: https://www.interviewbit.com/problems/window-string/

Given a string `S` and a string `T`, find the minimum window in `S` which will contain all the characters in `T` in linear time complexity.
 Note that when the count of a character C in `T` is N, then the count of C in minimum window in `S` should be at least N.

**Example :**

```
S = "ADOBECODEBANC"
T = "ABC"

```

Minimum window is `"BANC"`

> 
> 
> 
> **Note:**
> 
> - If there is no such window in S that covers all characters in T, return the empty string `''`.
> - If there are multiple such windows, return the first occurring minimum window ( with minimum start index ).

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
string Solution::minWindow(string A, string B) {
    string ans;
    if(B.length() > A.length()){
        return ans;
    }
    
    unordered_map<char, int> m;
    for(auto c:B){
        m[c]++;
    }
    
    int n = B.length();
    int max = INT_MAX;
    int p1 = 0, p2, flag = 0;
    unordered_map<char, int> freq;
    int start =0, end = 0, count = 0;
    
    for(int i =0; i<A.length(); i++){
        if(m.find(A[i]) != m.end()){
            freq[A[i]]++;
            if(freq[A[i]]<= m[A[i]]){
                count++;
            }
        }
        if(count == n){
            flag++;
            while(start<end){
                if(freq.find(A[start]) != freq.end()){
                    if(freq[A[start]]> m[A[start]]){
                        freq[A[start]]--;
                    }
                    else{
                        break;
                    }
                }
                start++;
            }
            if(max>(end - start + 1)){
                    max = end - start + 1;
                    p1 = start;
                    p2 = end;
                }
        }
        end++;
    }
    if(flag == 0){
        return ans;
    }
    ans = A.substr(p1, p2-p1 +1);
    return ans;
}
```