# Fraction | Interviewbit

Created: July 16, 2022 7:54 PM
Tags: Hashing
URL: https://www.interviewbit.com/problems/fraction/

Given two integers representing the numerator and denominator of a fraction, return the fraction in string format.

If the fractional part is repeating, enclose the repeating part in parentheses.

**Example :**

```
Given numerator = 1, denominator = 2, return "0.5"
Given numerator = 2, denominator = 1, return "2"
Given numerator = 2, denominator = 3, return "0.(6)"

```

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
string Solution::fractionToDecimal(int A, int B) {
    if(A == INT_MIN and B == -1) return "2147483648";
    int s = 0;
    long long x = A, y = B;
    if(A<0 and B>0 || A>0 and B<0) s = 1;
    x = abs(x);
    y = abs(y);
    
    string ans = to_string(x/y);
    if(s){
        ans = "-" + ans;
    }
    x = x%y;
    if(x == 0 ) return ans;
    ans += ".";
    
    map<pair<long long, long long>, long long> m;
    
    while(x!=0){
        x = x*10;
        int n = x/y;
        if(m.count(make_pair(x,y))!= 0){
            return ans.substr(0, m[make_pair(x,y)]) + '(' + ans.substr(m[make_pair(x,y)]) + ')';
        }
        
        m[make_pair(x,y)] = ans.size();
        x = x%y;
        ans += to_string(n);
    }
    return ans;
}
```