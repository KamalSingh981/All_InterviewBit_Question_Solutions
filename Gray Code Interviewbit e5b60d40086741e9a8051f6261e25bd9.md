# Gray Code | Interviewbit

Created: July 12, 2022 8:01 PM
Tags: Backtracking, Recursion
URL: https://www.interviewbit.com/problems/gray-code/

The gray code is a binary numeral system where two successive values differ in only one bit.

Given a non-negative integer `n` representing the total number of bits in the code, print the sequence of gray code. A gray code sequence must begin with `0`.

For example, given n = `2`, return `[0,1,3,2]`. Its gray code sequence is:

There might be multiple gray code sequences possible for a given n.
 Return any such sequence.

```cpp
vector<string> grayCodeInBinary(int A){
    // Base Case
    if(A == 1){
        vector<string> ans;
        ans.push_back("0");
        ans.push_back("1");
        return ans;
    }
    
    // Recursive Case
    vector<string> p = grayCodeInBinary(A -1);
    for(int i = 0; i<p.size(); i++){
        p[i] = "0" + p[i];
    }
    int n = p.size();
    for(int i = n-1; i>=0; i--){
        p.push_back("1" + p[i].substr(1, A-1));
    }
    return p; 
}

vector<int> Solution::grayCode(int A) {
    // Do not write main() function.
    // Do not read input, instead use the arguments to the function.
    // Do not print the output, instead return values as specified
    // Still have a doubt. Checkout www.interviewbit.com/pages/sample_codes/ for more details
    vector<string> a = grayCodeInBinary(A);
    vector<int> ans;
    for(int i=0; i<a.size(); i++){  
        ans.push_back(stoi(a[i], 0, 2));
    }
    return ans;
}
```