# Triplets with Sum between given range | Interviewbit

Created: May 13, 2022 1:33 AM
URL: https://www.interviewbit.com/problems/triplets-with-sum-between-given-range/

Given an array of real numbers greater than zero in form of strings.
 Find if there exists a **triplet** (a,b,c) such that **1** < **a+b+c** < **2** . 
 Return **1** for **true** or **0** for **false**.

**Example:**

Given [0.6, 0.7, 0.8, 1.2, 0.4] ,

You should return **1**

as

0.6+0.7+0.4=1.7

1<1.7<2

Hence, the output is 1.

**O(n)** solution is expected.

**Note**: You can assume the numbers in strings don’t overflow the primitive data type and there are no leading zeroes in numbers. Extra memory usage is allowed.

```cpp
class Solution:
	# @param A : list of strings
	# @return an integer
	def solve(self, A):
        n = len(A)
        B = [float(i) for i in A]
        buckets = [[], [], []]
        for i in B:
            if i < 2.0/3:
                buckets[0].append(i)
            elif i < 1:
                buckets[1].append(i)
            else:
                buckets[2].append(i)
        
        def get(index):
            amx1, amx2, amx3 = -10, -10, -10
            ami1, ami2, ami3 = 3, 3, 3
            for i in buckets[index]:
                if i > amx1:
                    amx1, amx2, amx3 = i, amx1, amx2
                elif i > amx2:
                    amx2, amx3 = i, amx2
                elif i > amx3:
                    amx3 = i
            
                if i < ami1:
                    ami1, ami2, ami3 = i, ami1, ami2
                elif i < ami2:
                    ami2, ami3 = i, ami2
                elif i < ami3:
                    ami3 = i
            return [amx1, amx2, amx3, ami1, ami2, ami3]
        
        
        a = get(0)
        b = get(1)
        c = get(2)
        ls = []
        fc = a[0] + a[1] + a[2]
        ls.append(fc)
        fc = a[3] + a[4] + c[3]
        ls.append(fc)
        fc = a[3] + b[3] + b[4]
        ls.append(fc)
        fc = a[3] + b[3] + c[3]
        ls.append(fc)
        fc = b[0] + a[3] + a[4]
        ls.append(fc)
        if a[0] != a[3]:
            fc = b[0] + a[0] + a[3]
            ls.append(fc)
            fc = b[3] + a[0] + a[3]
            ls.append(fc)
        fc = b[3] + a[0] + a[1]
        ls.append(fc)
        for fc in ls:
            if fc > 1 and fc < 2:
                return 1
        return 0
```