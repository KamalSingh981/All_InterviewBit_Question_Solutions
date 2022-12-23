# Pythagorean Triplets | Interviewbit

Created: May 9, 2022 1:39 AM
URL: https://www.interviewbit.com/problems/pythagorean-triplets/

**Problem Description**

A Pythagorean triplet is a set of three integers **a, b and c** such that **a2 + b2 = c2**.
Find the number of pythagorean triplets such that all the elements of the triplet are less than or equal to **A**.

**Problem Constraints**

**Input Format**

**Output Format**

**Example Input**

**Example Output**

**Example Explanation**

Explanation 1:

```
Then only triplet is {3, 4, 5}
```

Explanation 2:

```
The triplets are {3, 4, 5}, {6, 8, 10}, {5, 12, 13}.

```

```cpp
#include <cmath>
int Solution::solve(int A) {
    
    int ans;
    int c = 0;
    for(int i=1; i<=A; i++){
        for (int j=i+1; j<=A; j++){
            c = i*i + j*j;
            int x = sqrt(c);
            if(x*x == c && x<=A){
                ans += 1;
            }
        }
    }
    
    return ans;
}
```