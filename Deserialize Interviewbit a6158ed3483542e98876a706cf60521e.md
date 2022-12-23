# Deserialize | Interviewbit

Created: May 12, 2022 2:36 PM
URL: https://www.interviewbit.com/problems/deserialize/

**Problem Description**

You are given a string **A** which is a serialized string. You have to restore the original array of strings.
 The string in the output array should only have lowercase english alphabets.

Serialization: Scan each element in a string, calculate its length and append it with a string and a element separator or deliminator (the deliminator is ~). We append the length of the string so that we know the length of each element.

For example, for a string 'interviewbit', its serialized version would be 'interviewbit12~'.

**Problem Constraints**

**Input Format**

**Output Format**

**Example Input**

Input 1:

```
A = 'scaler6~academy7~'

```

Input 2:

```
A = 'interviewbit12~'

```

**Example Output**

Output 1:

```
['scaler', 'academy']

```

Output 2:

```
['interviewbit']

```

**Example Explanation**

Explanation 1:

```
Length of 'scaler' is 6 and academy is 7. So, the resulting string is scaler6~academy7~.
We hve to reverse the process.
```

Explanation 2:

```
Explained in the description above.

```

```python
class Solution:
    # @param A : string
    # @return a list of strings
    def deserialize(self, A):
        l = len(A)
        ans = []
        i = l-1
        s = ""
        for i in A:
            if(i.isalpha()):
                s+=i
            else:
                if s!="":
                    ans.append(s)
                s =""
        return ans
```