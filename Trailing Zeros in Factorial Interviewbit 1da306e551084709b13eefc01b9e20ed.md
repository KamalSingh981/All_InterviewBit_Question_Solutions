# Trailing Zeros in Factorial | Interviewbit

Created: May 9, 2022 10:35 PM
URL: https://www.interviewbit.com/problems/trailing-zeros-in-factorial/

**Problem Description**

Given an integer **A**, return the number of trailing zeroes in A!.

**Note**: Your solution should be in logarithmic time complexity.

**Problem Constraints**

**Input Format**

First and only argumment is integer A.

**Output Format**

**Example Input**

Input 1:

```
 A = 4

```

Input 2:

```
 A = 5

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 4! = 24

```

Explanation 2:

```
 5! = 120

```

```cpp
int Solution::trailingZeroes(int A) {
    int count = 0;
    // Counting the number of 5 in the given number:
    for(int i=5; i<=A; i = i=i*5){
        count += A/i;
    }
    return count;
}
```