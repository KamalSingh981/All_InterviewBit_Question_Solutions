# Longest Common Prefix | Interviewbit

Created: June 14, 2022 3:29 AM
Tags: String
URL: https://www.interviewbit.com/problems/longest-common-prefix/

**Problem Description**

Given the array of strings **A**, you need to find the longest string **S** which is the prefix of **ALL** the strings in the array.

Longest common prefix for a pair of strings **S1** and **S2** is the longest string **S** which is the prefix of both **S1** and **S2**.

**For Example:** longest common prefix of `"abcdefgh"` and `"abcefgh"` is `"abc"`.

**Input Format**

The only argument given is an array of strings A.

**Output Format**

Return the longest common prefix of all strings in A.

**Example Input**

Input 1:

```
A = ["abcdefgh", "aefghijk", "abcefgh"]
```

Input 2:

```
A = ["abab", "ab", "abcd"];
```

**Example Output**

Output 1:

```
"a"
```

Output 2:

```
"ab"
```

**Example Explanation**

Explanation 1:

```
Longest common prefix of all the strings is "a".
```

Explanation 2:

```
Longest common prefix of all the strings is "ab".
```

```cpp
string Solution::longestCommonPrefix(vector<string> &A) {
    string ans = "";
    int a = INT_MAX;
    for(int i = 0; i<A.size(); i++){
        if(a>A[i].length()){
            a = A[i].length();
        }
    }
    for(int j= 0; j<a; j++){
        for(int i=1; i<A.size(); i++){
            if(A[i-1][j] != A[i][j]){
                return ans;
            }
        }
        ans += A[0][j];
    }
    return ans;
}
```