# Letter Phone | Interviewbit

Created: July 2, 2022 12:20 AM
Tags: Recursion
URL: https://www.interviewbit.com/problems/letter-phone/

Given a digit string, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below.

![Letter%20Phone%20Interviewbit%2085471c093fe348e883b27d8a09d7e6a9/200px-Telephone-keypad2.svg.png](Letter%20Phone%20Interviewbit%2085471c093fe348e883b27d8a09d7e6a9/200px-Telephone-keypad2.svg.png)

The digit 0 maps to 0 itself.
 The digit 1 maps to 1 itself.

```
Input: Digit string "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].

```

Make sure the returned strings are lexicographically sorted.

```cpp
string stri[] = {"0", "1" , "abc", "def", "ghi", "jkl", "mno", "pqrs", "tuv", "wxyz"};

vector<string> Solution::letterCombinations(string A) {
    if(A.size() == 0){
        return {""};
    }
    
    char ch = A[0];
    string rem = A.substr(1);
    vector<string> recres = letterCombinations(rem);
    string s = stri[ch - '0'];
    vector<string> fi;
    
    
    for(int i = 0; i<s.size(); i++){
        char front  = s[i];
        for(auto it: recres){
            fi.push_back(front + it);
        }
    }
    
    return fi;
    
}
```