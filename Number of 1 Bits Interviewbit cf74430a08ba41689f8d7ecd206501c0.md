# Number of 1 Bits | Interviewbit

Created: May 26, 2022 2:18 AM
Tags: bit manipullation
URL: https://www.interviewbit.com/problems/number-of-1-bits/

**Problem Description**

**Problem Constraints**

**Input Format**

**Output Format**

**Example Input**

**Input1:**

```
    11

```

**Example Output**

**Output1:**

```
3

```

**Example Explanation**

**Explaination1:**

```
11 is represented as 1101 in binary

```

My code

```cpp
int num(unsigned int A){
    int ans = 0;
    for(int i = 0;i<32; i++){
        if((A&1) == 1){
            ans++;
        }
        A = A>>1;
    }
    return ans;
}

int Solution::numSetBits(unsigned int A) {
    return num(A);
}
```

Interviewbit Code

```cpp
int Solution::numSetBits(unsigned int n) {
    int count=0;
    while(n!=0)
    {
        n=n & (n-1);
        count++;
    }
    return count;
}
```