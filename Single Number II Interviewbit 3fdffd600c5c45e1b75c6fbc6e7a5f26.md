# Single Number II | Interviewbit

Created: May 28, 2022 2:02 AM
Tags: bit manipullation
URL: https://www.interviewbit.com/problems/single-number-ii/

Given an array of integers, every element appears thrice except for one which occurs once.

Find that element which does not appear thrice.

*Note: Your algorithm should have a linear runtime complexity.*

Could you implement it without using extra memory?

**Input Format:**

```
    First and only argument of input contains an integer array A

```

**Output Format:**

```
    return a single integer.

```

**Constraints:**

```
2 <= N <= 5 000 000
0 <= A[i] <= INT_MAX

```

**For Examples :**

```
Example Input 1:
    A = [1, 2, 4, 3, 3, 2, 2, 3, 1, 1]
Example Output 1:
    4
Explanation:
    4 occur exactly once
Example Input 2:
    A = [0, 0, 0, 1]
Example Output 2:
    1

```

```cpp
int Solution::singleNumber(const vector<int> &A) {
    int ones = 0;
    int twos = 0;
    for(int i =0; i<A.size(); i++){
        ones = (ones^A[i]) & (~twos);
        twos = (twos^A[i]) & (~ones);
    }
    return ones;
}
```

Algorithm 

First approach is to use a hash map  and return the element which have the value equal to 1.

In the second approach we can sort the array it will take O(nlogn) time and then we can traverse the array and where ever we find the single element we’ll return it.

In the third approach we are going to count the number of set bit in the binary representation of the number if they are of multiple of   3 then the set bit of ans is 0 esle 1 and doing this for all the 32 bits according to there weight.

In the fourth approach we are going to  the concept of bitmasking. It’s code is given above.