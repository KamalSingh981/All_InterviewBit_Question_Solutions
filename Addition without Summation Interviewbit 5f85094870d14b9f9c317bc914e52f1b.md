# Addition without Summation | Interviewbit

Created: May 9, 2022 1:58 AM
URL: https://www.interviewbit.com/problems/addition-without-summation/

**Problem Description**

You are given two numbers **A** and **B**.

You have to add them without using arithmetic operators and return their sum.

**Problem Constraints**

**Input Format**

**Output Format**

**Example Input**

Input 1:

```
A = 3
B = 10

```

Input 2:

```
A = 6
B = 1

```

**Example Output**

**Example Explanation**

Explanation 1:

```
3 + 10 = 13
```

Explanation 2:

```
6 + 1 = 7.
Note, you have to add without using arithmetic operators.

```

```cpp
int Solution::addNumbers(int A, int B) {
    while(B!=0){
            int carry = A&B;
            A = A^B;
            B = carry << 1;
}
return A;
}
```