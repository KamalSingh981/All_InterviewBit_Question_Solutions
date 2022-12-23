# Power Of Two Integers | Interviewbit

Created: May 16, 2022 1:42 PM
URL: https://www.interviewbit.com/problems/power-of-two-integers/

Given a positive integer which fits in a 32 bit signed integer, find if it can be expressed as A^P where P > 1 and A > 0. A and P both should be integers.

**Example**

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```python
class Solution:
	# @param A : integer
	# @return an integer
	def isPower(self, A):
        if(A==1):
            return 1
        
        i = 2
        while(i*i<=A):
            if((math.log(A)/math.log(i))%1 < 0.00000001):
                return 1
            i +=1     
        return 0
```