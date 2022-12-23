# Implement StrStr | Interviewbit

Created: June 14, 2022 2:02 PM
Tags: String
URL: https://www.interviewbit.com/problems/implement-strstr/

Another question which belongs to the category of questions which are intentionally stated vaguely. 
 Expectation is that you will ask for correct clarification or you will state your assumptions before you start coding.

**Problem Description**

Another question which belongs to the category of questions which are intentionally stated vaguely.

Expectation is that you will ask for correct clarification or you will state your assumptions before you start coding.

**Implement strStr().**
 strstr - locate a substring ( needle ) in a string ( haystack ).

**Try not to use standard library string functions for this question.**

Returns the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

**NOTE:** String A is haystack, B is needle.

**Good clarification questions:**

1. What should be the return value if the needle is empty?
2. What if both haystack and needle are empty?

For the purpose of this problem, assume that the return value should be -1 in both cases.

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
int Solution::strStr(const string A, const string B) {
    if(B=="" || A=="" && B==""){
        return -1;
    }
    for(int i=0; i<A.length(); i++){
        if(A[i] == B[0]){
            int q = 1;
            while(q<B.length()){
                if(A[i+q]!=B[q]){
                    break;
                }
                else{
                    q++;
                }
            }
            if(q == B.length()){
                return i;
            }
        }
    }
    return -1;
}
```