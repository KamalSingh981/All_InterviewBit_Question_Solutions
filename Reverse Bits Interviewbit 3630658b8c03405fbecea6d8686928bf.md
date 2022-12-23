# Reverse Bits | Interviewbit

Created: May 26, 2022 3:10 AM
Tags: bit manipullation
URL: https://www.interviewbit.com/problems/reverse-bits/

**Problem Description**

Reverse the bits of an **32** bit unsigned integer A.

**Problem Constraints**

**Input Format**

First and only argument of input contains an integer A.

**Output Format**

Return a single unsigned integer denoting the decimal value of reversed bits.

**Example Input**

Input 1:

```
 0
```

Input 2:

```
 3
```

**Example Output**

Output 1:

```
 0
```

Output 2:

```
 3221225472
```

**Example Explanation**

Explanation 1:

```
        00000000000000000000000000000000

=>      00000000000000000000000000000000

```

Explanation 2:

```
        00000000000000000000000000000011
=>      11000000000000000000000000000000

```

```cpp
unsigned int Solution::reverse(unsigned int A) {
   unsigned int ans = 0;
   for(int i = 31; i>=0; i--){
       if(A&1){
       ans += (1<<i);
       }
       A = A>>1;
   } 
   return ans;
}
```