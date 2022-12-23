# Remove Consecutive Characters | Interviewbit

Created: June 14, 2022 3:11 AM
Tags: String
URL: https://www.interviewbit.com/problems/remove-consecutive-characters/

**Problem Description**

Given a string **A** and integer **B**, remove all consecutive same characters that have length exactly B.

**Problem Constraints**

**Input Format**

First Argument is string A.

Second argument is integer B.

**Output Format**

Return a string after doing the removals.

**Example Input**

Input 1:

```
A = "aabcd"
B = 2

```

Input 2:

```
A = "aabbccd"
B = 2

```

**Example Output**

Output 1:

```
 "bcd"

```

Output 2:

```
 "d"

```

**Example Explanation**

Explanation 1:

```
 "aa" had length 2.

```

Explanation 2:

```
 "aa", "bb" and "cc" had length of 2.

```

```cpp
string Solution::solve(string A, int B) {
    int count = 1;
    int index = 1;
    int n = A.size();
    char temp = A[0];
    for(int i = 1; i<n; i++){
        if(temp == A[index]){
            count++;
            index++;
        }
        else{
            temp = A[index];
            count = 1;
            index++;
        }
        if(count == B){
            A.erase(index-B, B);
            index -= B;
            count = 0;
        }
    }
    return A;
}
```