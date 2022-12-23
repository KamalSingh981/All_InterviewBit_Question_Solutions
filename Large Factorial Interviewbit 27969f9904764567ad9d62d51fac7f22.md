# Large Factorial | Interviewbit

Created: May 9, 2022 1:42 AM
Tags: Number Theory
URL: https://www.interviewbit.com/problems/large-factorial/

**Problem Description**

Given a number **A**. Find the fatorial of the number.

**Problem Constraints**

**Input Format**

First and only argument is the integer A.

**Output Format**

Return a string, the factorial of A.

**Example Input**

Input 1:

```
A = 2

```

Input 2:

```
A = 3

```

**Example Output**

Output 1:

```
 2

```

Output 2:

```
 6

```

**Example Explanation**

Explanation 1:

```
2! = 2 .

```

Explanation 2:

```
3! = 6 .

```

```cpp
string Solution::solve(int N) {
    int carry, size, mul;
    int arr[1000];
    arr[0]=1;
    size = 1;
    carry = 0;
    for (int i=2; i<=N; i++){
        for (int j=0; j<size; j++){
            mul = arr[j]*i + carry;
            arr[j] = mul%10;
            carry = mul/10;
        }
        while(carry>0){
            arr[size] = carry%10;
            size += 1;
            carry /=10;

        }
    }
    string ans = "";
    for(int k = size-1; k>= 0; k--){
        ans += to_string(arr[k]);
    }

    return ans;
}
```