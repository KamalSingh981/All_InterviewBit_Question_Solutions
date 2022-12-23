# Multiply Strings | Interviewbit

Created: June 15, 2022 4:20 PM
Tags: String
URL: https://www.interviewbit.com/problems/multiply-strings/

Given two numbers represented as strings, return multiplication of the numbers as a string.

> 
> 
> 
> **Note:** The numbers can be arbitrarily large and are non-negative. **Note2:** Your answer should not have leading zeroes. For example, `00` is not a valid answer.
> 

For example, 
 given strings `"12", "10"`, your answer should be “120”.

**NOTE** : DO NOT USE BIG INTEGER LIBRARIES ( WHICH ARE AVAILABLE IN JAVA / PYTHON ). 
 We will retroactively disqualify such submissions and the submissions will incur penalties.

```python
string multi(string A, char n){
    int q = n - '0';
    reverse(A.begin(), A.end());
    int carry = 0;
    for(int i = 0; i<A.length(); i++){
        int d = (carry + (A[i] -'0')*q)/10;
        A[i] = (carry + (A[i] -'0')*q)%10 + '0';
        carry = d;
    }
    if(carry!=0){
        A += carry + '0';
    }
    reverse(A.begin(), A.end());
    return A;
}
string add(string A, string B){
    int carry = 0;
    int i = A.length() - 1;
    int j = B.length() - 1;
    string ans = "";
    while(i >= 0 || j >= 0){
        int sum = carry;
        if(i>=0) sum += A[i] - '0';
        if(j>=0) sum += B[j] - '0';
        ans  += sum%10 + '0';
        carry  = sum/10;
        i--;
        j--;
    }
    if(carry!=0){
        ans += carry + '0';
    }
    reverse(ans.begin(), ans.end());
    return ans;
}
string prod(string A, string B){
    string ans = "";
    string zero = "";
    for(int i=B.length()-1; i>=0; i--){
        string d = multi(A, B[i]);
        d += zero;
        ans = add(ans, d);
        zero += '0';
    }
    return ans;
}
string Solution::multiply(string A, string B) {
    if(A=="0" || B=="0"){
        return "0";
    }
    string d= prod(A,B);
    int i = 0;
    while(d[i]=='0'){
        i++;
    }
    d.erase(0,i);
    return d;
}
```

Interviewbit Code

```python
string Solution::multiply(string A, string B) 
{
    if (A=="0" || B=="0")
        return "0";
        
    int aL = A.length(), bL = B.length();
    vector<int> result(aL+bL, 0);
    string res = "";
    
    for (auto i=aL-1; i>=0; --i)
    {
        for (auto j=bL-1; j>=0; --j)
        {
            result[i+j+1] += (A[i] - '0')*(B[j] - '0');
        }
    }
    
    for (auto k=aL+bL-1; k>0; --k)
    {
        if (result[k] >= 10)
        {
            result[k-1] += result[k]/10;
            result[k] %= 10;
        }
    }
    
    int cnt = 0;
    for (auto l=0; l<result.size(); ++l)
    {
        if (result[l]==0 && l==cnt) //To omit the leading zeroes E.g. 00456723 will be 456723.
            ++cnt;
        else
            res += result[l] + '0'; //I was doing "-0" it was throwing internal error!
    }
    return res;

}
```

python code

```python
class Solution:
	# @param A : string
	# @param B : string
	# @return a strings
	def multiply(self, A, B):
        return str(int(A)*int(B))
```