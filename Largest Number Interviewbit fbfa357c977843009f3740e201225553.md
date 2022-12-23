# Largest Number | Interviewbit

Created: May 14, 2022 11:30 PM
Tags: String
URL: https://www.interviewbit.com/problems/largest-number/

Given a list of non negative integers, arrange them such that they form the largest number.

**For example:**

Given `[3, 30, 34, 5, 9]`, the largest formed number is `9534330`.

*Note: The result may be very large, so you need to retusrn a string instead of an integer.*

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
#include <bits/stdc++.h>
int compare(string x, string y){
    string xy = x.append(y);
    string yx = y.append(x);
    return xy.compare(yx) > 0 ? 1 : 0;
}
string Solution::largestNumber(const vector<int> &A) {
    if(accumulate(A.begin(), A.end(), 0) == 0){
        return "0";
    }
    vector<string> a(A.size());
    for(int i =0; i<a.size(); i++){
         a[i] = to_string(A[i]);
         
    }
    sort(a.begin(), a.end(), compare);

    string ans;
    for(int i =0; i<a.size(); i++){
         ans+= a[i];
      }

     return ans;
}
```