# Power of 2 | Interviewbit

Created: June 15, 2022 2:51 PM
Tags: String
URL: https://www.interviewbit.com/problems/power-of-2/

Find if Given number is power of 2 or not. 
 More specifically, find if given number can be expressed as 2^k where k >= 1.

**Input:**

```
number length can be more than 64, which mean number can be greater than 2 ^ 64 (out of long long range)

```

**Output:**

```
return 1 if the number is a power of 2 else return 0

```

**Example:**

```
Input : 128
Output : 1

```

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
int Solution::power(string A) {
    int i, n, sum=0, c;
    n = A.size();
    if(n==0) return 0;
    for(i=0; i<n; i++){
        sum += A[i] - '0';
    }
    
    if(sum ==1 && n==1){
        return 0;
    }
    while(!((A[n-1]-'0')&1)){
        for(i = 0, c= 0; i<n; i++){
            sum = c*10 + (A[i] -'0');
            A[i] = (sum/2) + '0';
            c = sum%2;
        }
    }
    
    for(i = 0, sum = 0; i<n; i++){
        sum += (A[i] - '0');
    }
    if(sum == 1){
        return 1;
    }
    return 0;   
}
```

```python
class Solution:
	# @param A : string
	# @return an integer
	def power(self, A):
        s = "{0:b}".format(int(A))
        if(s == "1"):
            return 0
        else:
            for i in range(1, len(s)):
                if(s[i] == '1'):
                    return 0 
        return 1
```