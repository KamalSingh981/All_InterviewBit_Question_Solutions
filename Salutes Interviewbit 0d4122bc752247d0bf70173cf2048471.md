# Salutes | Interviewbit

Created: May 10, 2022 1:03 AM
URL: https://www.interviewbit.com/problems/salutes/

**Problem Description**

In a long hallway some soldiers are walking from left to right and some from right to left all at the same speed.
 Every time while walking they cross through another soldier they salute and move ahead.
 Given a string **A** of length **N** showing the soldiers' direction they are walking. **'<'** denotes a soldier is walking from right to left, and **'>'** denotes a soldier is walking from left to right. Return the number of Salutes done.

**Problem Constraints**

**Input Format**

**Output Format**

**Example Input**

Input 1:

```
A = '>>><<<'

```

Input 2:

```
A = '<>'

```

**Example Output**

**Example Explanation**

Explanation 1:

```
Soldier 1 will salute with 4, 5, 6. Same goes for soldier 2 and 3.
Hence, the total number of salutes is 9.
```

Explanation 2:

```
There will be no salutes as no two soldiers will cross each other.

```

```cpp
long Solution::countSalutes(string A) {
    int l = A.length();
    long ans = 0;
    long right = 0;
    for(int i=0; i<l; i++){
        if('>' == A[i]){
            right+=1;
        }
        else{
            ans += right;
        }
    }

    return ans;
}
```