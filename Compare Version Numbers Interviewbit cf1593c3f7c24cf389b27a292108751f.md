# Compare Version Numbers | Interviewbit

Created: June 17, 2022 1:58 AM
Tags: String
URL: https://www.interviewbit.com/problems/compare-version-numbers/

Compare two version numbers version1 and version2.

> 
> 
> - If version1 > version2 return 1,
> - If version1 < version2 return -1,
> - otherwise return 0.

You may assume that the version strings are non-empty and contain only digits and the `.` character.
 The `.` character does not represent a decimal point and is used to separate number sequences.
 For instance, `2.5` is not `"two and a half"` or `"half way to version three"`, it is the fifth second-level revision of the second first-level revision.

Here is an example of version numbers ordering:

```python
class Solution:
	# @param A : string
	# @param B : string
	# @return an integer
	def compareVersion(self, A, B):
        c = A.split('.')
        d = B.split('.')
        c = list(map(int, c))
        d = list(map(int, d))
        if(len(c) >len(d)):
            for i in range(len(d), len(c)):
                d.append(0)
        else:
            for i in range(len(c), len(d)):
                c.append(0)
        for i in range(len(c)):
            if(c[i]>d[i]):
                return 1
            elif c[i]<d[i]:
                return -1
        return 0
```