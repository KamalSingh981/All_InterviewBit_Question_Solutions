# Add Binary Strings | Interviewbit

Created: June 15, 2022 2:51 AM
Tags: String
URL: https://www.interviewbit.com/problems/add-binary-strings/

**Problem Description**

Given two binary strings, return their sum (also a binary string).

**Example:**

```
a = "100"

b = "11"
Return a + b = "111".

```

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
string Solution::addBinary(string A, string B) {
    string ans = "";
    int a = A.length() - 1;
    int b = B.length() -1;
    int sum;
    int carry = 0;
    while(a>=0 || b>=0){
        sum = carry;
        if(a>=0) sum += A[a] - '0';
        if(b>=0) sum += B[b] - '0';
        ans += to_string(sum%2);
        carry = sum/2;
        a--;
        b--;
    }
    if(carry){
        ans += '1';
    }
    reverse(ans.begin(), ans.end());
    return ans;
}
```