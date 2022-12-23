# Check Palindrome! | Interviewbit

Created: June 20, 2022 3:06 AM
Tags: Hashing
URL: https://www.interviewbit.com/problems/check-palindrome/

**Problem Description**

Given a string **A** consisting of lowercase characters.

Check if characters of the given string can be rearranged to form a **palindrome**.

Return 1 if it is possible to rearrange the characters of the string **A** such that it becomes a palindrome else return 0.

**Problem Constraints**

1 <= |A| <= 105

A consists only of lower-case characters.

**Input Format**

First argument is an string **A**.

**Output Format**

Return 1 if it is possible to rearrange the characters of the string **A** such that it becomes a palindrome else return 0.

**Example Input**

Input 1:

```
 A = "abcde"

```

Input 2:

```
 A = "abbaee"

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 No possible rearrangement to make the string palindrome.

```

Explanation 2:

```
 Given string "abbaee" can be rearranged to "aebbea" to form a palindrome.

```

```cpp
int Solution::solve(string A) {
    map<char, int> a;
    for(char c: A){
        a[c]++;
    }
    int count = 0;
    for(auto d: a){
        if((d.second)%2){
            count++;
        }
    }
    if(count>1){
            return 0;
        }
    return 1;
}
```