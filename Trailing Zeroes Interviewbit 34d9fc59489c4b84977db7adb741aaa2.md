# Trailing Zeroes | Interviewbit

Created: May 25, 2022 5:33 PM
Tags: bit manipullation
URL: https://www.interviewbit.com/problems/trailing-zeroes/

**Problem Description**

Given an integer **A**, count and return the number of trailing zeroes.

**Problem Constraints**

**Input Format**

First and only argument is an integer A.

**Output Format**

Return an integer denoting the count of trailing zeroes.

**Example Input**

Input 1:

```
 A = 18
```

Input 2:

```
 A = 8
```

**Example Output**

Output 1:

```
 1
```

Output 2:

```
 3
```

**Example Explanation**

Explanation 1:

```
 18 in binary is represented as: 10010, there is 1 trailing zero.
```

Explanation 2:

```
 8 in binary is represented as: 1000, there are 3 trailing zeroes.
```

```cpp
int Solution::solve(int A) {
    int ans = 0;
    for(int j=0; j<32; j++){
            if((A&1) == 0){
                ans++;
            }
            else{
                break;
            }
            A = A>>1;
        }
    return ans;
}
```