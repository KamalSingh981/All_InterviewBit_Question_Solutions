# Maximal String | Interviewbit

Created: July 12, 2022 8:04 PM
Tags: Backtracking, Recursion
URL: https://www.interviewbit.com/problems/maximal-string/

**Problem Description**

Given a string **A** and integer **B**, what is maximal lexicographical string that can be made from A if you do atmost B swaps.

**Problem Constraints**

1 <= |A| <= 9

A contains only digits from 0 to 9.

1 <= B <= 5

**Input Format**

First argument is string A.

Second argument is integer B.

**Output Format**

Return a string, the naswer to the problem.

**Example Input**

Input 1:

```
A = "254"
B = 1

```

Input 2:

```
A = "254"
B = 2

```

**Example Output**

Output 1:

```
 524

```

Output 2:

```
 542

```

**Example Explanation**

Explanation 1:

```
 Swap 2 and 5.

```

Explanation 2:

```
Swap 2 and 5 then swap 4 and 2.

```

```cpp
string ans = "";
void findTheMaximum(string A, int B){
    // Base case
    if(B == 0){
        if(ans<A) ans = A;
        return;
    }
    
    for(int i = 0; i<A.length(); i++){
        for(int j = i+1; j<A.length(); j++){
            swap(A[i], A[j]);
            findTheMaximum(A, B-1);
            swap(A[i], A[j]);
        }
    }
}

string Solution::solve(string A, int B) {
    ans = "";
    findTheMaximum(A, B);
    return ans;
    
    
    
}
```