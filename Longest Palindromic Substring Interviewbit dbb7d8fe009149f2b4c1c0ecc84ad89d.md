# Longest Palindromic Substring | Interviewbit

Created: June 17, 2022 12:58 AM
Tags: String
URL: https://www.interviewbit.com/problems/longest-palindromic-substring/

**Problem Description**

Given a string A of size N, find and return the **longest palindromic substring** in A.

Substring of string A is `A[i...j]` where 0 <= i <= j < len(A)

**Palindrome string:**
 A string which reads the same backwards. More formally, A is palindrome if reverse(A) = A.

**Incase of conflict**, return the substring which occurs first ( with the least starting index).

**Input Format**

First and only argument is a string A.

**Output Format**

Return a string denoting the longest palindromic substring of string A.

**Example Input**

**Example Output**

**Example Explanation**

```
We can see that longest palindromic substring is of length 7 and the string is "aaabaaa".
```

```python
int extractingpalindrom(string s, int left, int right){
    if(s.length() < 1) return 0;
    while(left>=0 && right<s.length() && s[left] == s[right]){
        left--;
        right++;
    }
    return right - left - 1;
}

string Solution::longestPalindrome(string s) {
     int start = 0;
     int end = 0;
     int len = 0;
     for(int i = 0; i<s.length(); i++){
         int len1 = extractingpalindrom(s, i,i);
         int len2 = extractingpalindrom(s, i, i+1);
         len = max(len1, len2);
         if(len>(end - start+1)){
             start = i - ((len-1)/2);
             end = i + ((len)/2);
         }
     }    
     return s.substr(start, end- start +1);
}
```

```cpp
int Solution::compareVersion(string A, string B) {
    // Do not write main() function.
    // Do not read input, instead use the arguments to the function.
    // Do not print the output, instead return values as specified
    // Still have a doubt. Checkout www.interviewbit.com/pages/sample_codes/ for more details
    int j, i;
    for( i=0, j=0 ; i<A.size() || j<B.size() ; i++, j++){
        unsigned long long num1 = 0, num2 = 0;
        while(i < A.size() && A[i] != '.'){
            num1 *= 10;
            num1 += A[i] - '0';
            i++;
        }
        while(j < B.size() && B[j] != '.'){
            num2 *= 10;
            num2 += B[j] - '0';
            j++;
        }
        if(num1 > num2) return 1;
        if(num1 < num2) return -1;
    }
    return 0;
}
```