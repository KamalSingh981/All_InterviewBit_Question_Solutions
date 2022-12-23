# Max Continuous Series of 1s | Interviewbit

Created: June 13, 2022 11:01 PM
Tags: Two pointers
URL: https://www.interviewbit.com/problems/max-continuous-series-of-1s/

You are given with an array of `1s` and `0s`. And you are given with an integer `M`, which signifies number of flips allowed.
 Find the position of `zeros` which when flipped will produce `maximum continuous series of 1s`.

**For this problem, return the indices of `maximum continuous series of 1s` in order.**

**Example:**

```
Input :
Array = {1 1 0 1 1 0 0 1 1 1 }
M = 1

Output :
[0, 1, 2, 3, 4]

```

If there are multiple possible solutions, return the sequence which has the minimum start index.

```cpp
vector<int> Solution::maxone(vector<int> &A, int B) {
    int i = 0;
    int j = 0;
    int ans = 0;
    int a = 0;
    int b = 0;
    int flip = 0;
    int n = A.size();
    while(i<n){
        if(A[i]==0){
            flip++;
        }
        while(flip > B){
            if(A[j] == 0){
                flip--;
            }
            j++;
        }
        if(ans<(i - j + 1)){
            a = j;
            b = i;
            ans = i - j + 1;
        }
        i++;
    }
    vector<int> result;
    while(a<=b){
        result.push_back(a);
        a++;
    }
    return result;
}
```

Algorithm for this question is same as used in [https://www.notion.so/Maximum-Ones-After-Modification-Interviewbit-567c97556123414aa30643d56aaef055](Maximum%20Ones%20After%20Modification%20Interviewbit%20567c97556123414aa30643d56aaef055.md) i.e. sliding window.