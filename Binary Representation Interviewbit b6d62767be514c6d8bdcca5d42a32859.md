# Binary Representation | Interviewbit

Created: May 12, 2022 12:54 AM
URL: https://www.interviewbit.com/problems/binary-representation/

Given a number N >= 0, find its representation in binary.

**Example:**

if N = 6,

binary form = 110

**Problem Approach:**

Complete code in the hint.

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
string Solution::findDigitsInBinary(int A) {
    string s="";
    if(A==0){
        return "0";
    }
    while(A!=0){
        s += to_string(A%2);
        A /= 2;
    }
    reverse(s.begin(), s.end());
    return s;
}
```