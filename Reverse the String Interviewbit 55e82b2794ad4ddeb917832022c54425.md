# Reverse the String | Interviewbit

Created: June 15, 2022 12:19 AM
Tags: String
URL: https://www.interviewbit.com/problems/reverse-the-string/

Given a string **A**.

Return the string **A** after reversing the string word by word.

**NOTE**:

1. 
    
    A sequence of non-space characters constitutes a word.
    
2. 
    
    Your reversed string **should not contain leading or trailing spaces**, even if it is present in the input string.
    
3. 
    
    If there are multiple spaces between words, reduce them to a single space in the reversed string.
    

**Input Format**

```
The only argument given is string A.

```

**Output Format**

```
Return the string A after reversing the string word by word.

```

**For Example**

```
Input 1:
    A = "the sky is blue"
Output 1:
    "blue is sky the"

Input 2:
    A = "this is ib"
Output 2:
    "ib is this"

Input 3:
 A = " hello world "
Output 3:
 "world hello"
```

```cpp
string Solution::solve(string A) {
    string ans = "";
    int start = A.length();
    int end = A.length();
    int count = 0;
    for(int i=A.length()-1; i>=0; i--){
        if((A[i-1] == ' ' && A[i] != ' ') || i == 0){
            ans += A.substr(i, count+1) + ' ';
            count = 0;
        }
        else if (A[i] != ' '){
            count++;
        }
    }
    int i = ans.length()-1;
    while(!isalpha(ans[i])){
        ans.erase(i,1);
        i--;
    }
    return ans;
```