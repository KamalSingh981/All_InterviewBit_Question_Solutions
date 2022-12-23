# Palindrome Numbers | Interviewbit

Created: May 20, 2022 12:56 AM
Tags: Math
URL: https://www.interviewbit.com/problems/palindrome-numbers/

**Problem Description**

Given two integers **A** and **B** which represent an integer range **[A, B]**.
Find the **maximum** number of distinct **palindromic integers** we can take from the given range,
 such that the **absolute difference** between any **two integers** doesn't exceed **C**.

**Problem Constraints**

**Input Format**

The first argument is an integer A.
The second argument is an integer B.
The third argument is an integer C.

**Output Format**

**Example Input**

Input 1:

```
A = 80
B = 110
C = 10

```

Input 2:

```
A = 1
B = 10
C = 10

```

**Example Output**

**Example Explanation**

Explanation 1:

```
The plaindromic integers are 88, 99, 101.
We will pick 99, 101.
```

Explanation 2:

```
The plaindromic integers are 1, 2, 3, 4, 5, 6, 7, 8, 9.
We can pick all the palindrome integers.
```

```python
int ispalindrome(int a){
    int rev = 0;
    for(int i=a; i>0; i/=10){
        rev = i%10 + rev*10;
    }
    return rev==a;
}

int Solution::solve(int A, int B, int C) {
    vector<int> res;
    for(int i=A; i<=B; i++){
        if(ispalindrome(i)){
            res.push_back(i);
        }
    }

    int l=0, r =0;
    int n = res.size();
    int ans = 0;
    while(r<n){
        while(r<n && res[r]-res[l]<=C){
            r++;
        }
        ans = max(ans, r-l);
        if(r==n){
            break;
        }

        while(l<n && res[r]- res[l]>C){
            l++;
        }
    }

    return ans;

}
```