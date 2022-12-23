# Longest Consecutive Sequence | Interviewbit

Created: July 17, 2022 2:03 AM
Tags: Hashing
URL: https://www.interviewbit.com/problems/longest-consecutive-sequence/

Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

**Example:** 
 Given `[100, 4, 200, 1, 3, 2]`,
 The longest consecutive elements sequence is `[1, 2, 3, 4]`. Return its length: `4`.

Your algorithm should run in `O(n)` complexity.

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
int Solution::longestConsecutive(const vector<int> &A) {
    map<int, int> m;
    for(int i = 0; i<A.size(); i++){
        m[A[i]]=1;
    }
    int ans = 1;
    int count = 0;
    bool flag = true;
    for(auto s:m){
        if(flag){
            flag = false;
        }
        else{
            if(m.find(s.first-1) != m.end()){
                count++;
            }
            else{
                count = 0;
            }
        }
        ans = max(ans, count+1);
    }
    return ans;
}
```