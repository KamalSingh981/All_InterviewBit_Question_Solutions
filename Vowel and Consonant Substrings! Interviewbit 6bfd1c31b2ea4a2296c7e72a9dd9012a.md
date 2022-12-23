# Vowel and Consonant Substrings! | Interviewbit

Created: June 14, 2022 2:12 AM
Tags: String
URL: https://www.interviewbit.com/problems/vowel-and-consonant-substrings/

**Problem Description**

Given a string **A** consisting of lowercase characters.

You have to find the number of substrings in **A** which starts with **vowel** and end with **consonants** or vice-versa.

Return the count of substring modulo **109 + 7**.

**Problem Constraints**

1 <= |A| <= 105

A consists only of lower-case characters.

**Input Format**

First argument is an string **A**.

**Output Format**

Return a integer denoting the the number of substrings in **A** which starts with **vowel** and end with **consonants** or vice-versa with modulo **109 + 7**.

**Example Input**

Input 1:

```
 A = "aba"

```

Input 2:

```
 A = "a"

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 Substrings of S are : [a, ab, aba, b, ba, a]Out of these only 'ab' and 'ba' satisfy the condition for special Substring. So the answer is 2.

```

Explanation 2:

```
 No possible substring that start with vowel and end with consonant or vice-versa.

```

```cpp
int Solution::solve(string A) {
    long long v=0;
    long long c=0;
    long long ans=0;
    long long mode=1000000007;
    for(int i=0;i<A.size();i++)
    {
        if(A[i]=='a'||A[i]=='e'||A[i]=='i'||A[i]=='o'||A[i]=='u')
        {
            v++;
            ans= (ans+c)%mode;
        }
        else
        {
            c++;
            ans=(ans+v)%mode;
        }
    }
    return (int)ans;
}
```