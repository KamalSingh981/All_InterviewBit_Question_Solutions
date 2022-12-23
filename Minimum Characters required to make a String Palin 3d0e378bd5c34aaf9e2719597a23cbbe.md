# Minimum Characters required to make a String Palindromic | Interviewbit

Created: June 16, 2022 6:40 PM
Tags: String
URL: https://www.interviewbit.com/problems/minimum-characters-required-to-make-a-string-palindromic/

Given an string **A**. The only operation allowed is to insert characters in the beginning of the string.

Find how many minimum characters are needed to be inserted to make the string a palindrome string.

**Input Format**

```
The only argument given is string A.

```

**Output Format**

```
Return the minimum characters that are needed to be inserted to make the string a palindrome string.

```

**For Example**

```
Input 1:
    A = "ABC"
Output 1:
    2
    Explanation 1:
        Insert 'B' at beginning, string becomes: "BABC".
        Insert 'C' at beginning, string becomes: "CBABC".

Input 2:
    A = "AACECAAAA"
Output 2:
    2
    Explanation 2:
        Insert 'A' at beginning, string becomes: "AAACECAAAA".
        Insert 'A' at beginning, string becomes: "AAAACECAAAA".

```

```python
int Solution::solve(string A) {
    string d = A;
    reverse(A.begin(), A.end());
    d = d + '#' + A;
    int j = 0;
    vector<int> lps(d.size(), 0);
    for(int i= 1; i<d.size(); i++){
        if(d[i] == d[j]){
            j++;
            lps[i] = j;
        }
        else{
            if(j != 0){
                j = lps[j-1];
                i--;
            }
            else{
                lps[i] = 0;
            }     
        }
    }  
    return A.size() - lps.back(); 
}
```

Algorithm 

It uses KMP algorithm to find the LPS array of a string formed by the concatenation of original string special character and reverse original string.