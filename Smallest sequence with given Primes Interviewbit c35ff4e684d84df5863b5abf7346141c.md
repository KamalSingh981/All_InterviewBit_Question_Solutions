# Smallest sequence with given Primes | Interviewbit

Created: August 8, 2022 3:01 AM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/smallest-sequence-with-given-primes/

**Problem Description**

Given three prime numbers **A, B** and **C** and an integer **D**.

You need to find the first(smallest) **D** integers which only have **A, B, C** or a combination of them as their prime factors.

**Input Format**

First argument is an integer **A**.

Second argument is an integer **B**.

Third argument is an integer **C**.

Fourth argument is an integer **D**.

**Output Format**

Return an array of size `D` denoting the first smallest **D** integers which only have **A, B, C** or a combination of them as their prime factors.

**NOTE:** You need to return the array sorted in ascending order.

**Example Input**

Input 1:

```
 A = 2
 B = 3
 C = 5
 D = 5

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 4 = A * A i.e ( 2 * 2 )
 6 = A * B i.e ( 2 * 3 )

```

```cpp
vector<int> Solution::solve(int a, int b, int c, int D) {
    vector<int> ans;
    ans.push_back(1);
    int i = 0, j = 0, k = 0;
    while(D--){
        int x = min(min(ans[i]*a, ans[j]*b), ans[k]*c);
        ans.push_back(x);
        if(x == ans[i]*a){
            i++;
        }
        if(x == ans[j]*b){
            j++;
        }
        if(x == ans[k]*c){
            k++;
        }
    }
    ans.erase(ans.begin());
    return ans;
}
```