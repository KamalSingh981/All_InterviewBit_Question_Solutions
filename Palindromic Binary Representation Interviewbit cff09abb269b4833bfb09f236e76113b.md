# Palindromic Binary Representation | Interviewbit

Created: June 16, 2022 12:54 AM
Tags: bit manipullation
URL: https://www.interviewbit.com/problems/palindromic-binary-representation/

**Problem Description**

Given an integer **A** find the **Ath** number whose binary representation is a palindrome.

**NOTE:**

- Consider the 1 number whose binary representation is palindrome as 1, instead of 0
    
    st
    
- Do not consider the leading zeros, while considering the binary representation.

**Problem Constraints***Input Format*

*First and only argument is an integer **A**.*

*Output Format*

*Return an integer denoting the **Ath** number whose binary representation is a palindrome.*

*Example Input*

*Input 1: 

 `A = 1`
 
Input 1: 

 `A = 9`*

*Example Output*

*Example Explanation*

- 

Explanation 1:

```
 1st Number whose binary representation is palindrome is 1

```

Explanation 2

```
 9th Number whose binary representation is palindrome is 27 (11011)

```

```python
// C++ program to find n-th palindrome
#include <bits/stdc++.h>
using namespace std;
 
// utility function which is used to
// convert binary string into integer
int convertStringToInt(string s)
{
    int num = 0;
 
    // convert binary string into integer
    for (int i = 0; i < s.size(); i++) {
        num = num * 2 + (s[i] - '0');
    }
    return num;
}
 
// function to find nth binary palindrome number
int getNthNumber(int n)
{
 
    // base case
    if (n == 1)
        return 1;
    n--;
 
    // stores the binary palindrome string
    queue<string> q;
 
    // add 2nd binary palindrome string
    q.push("11");
 
    // runs till the nth binary palindrome number
    while (!q.empty()) {
        // remove curr binary palindrome string from queue
        string curr = q.front();
        q.pop();
        n--;
 
        // if n==0 then we find the n'th binary palindrome
        // so we return our answer
        if (!n) {
            return convertStringToInt(curr);
        }
 
        int mid = curr.size() / 2;
 
        // if length is even .so it is our first case
        // we have two choices
        if (curr.size() % 2 == 0) {
            string s0 = curr, s1 = curr;
            s0.insert(mid, "0");
            s1.insert(mid, "1");
            q.push(s0);
            q.push(s1);
        }
         
        // if length is odd .so it is our second case
        // we have only one choice
        else {
            string ch(1, curr[mid]);
            string temp = curr;
            temp.insert(mid, ch);
            q.push(temp);
        }
    }
 
    return 0;
}
int Solution::solve(int A) {
    return getNthNumber(A);
}
```