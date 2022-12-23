# Subarray with given XOR | Interviewbit

Created: July 15, 2022 9:56 PM
Tags: Hashing
URL: https://www.interviewbit.com/problems/subarray-with-given-xor/

**Problem Description**

Given an array of integers **A** and an integer **B**.

Find the total number of subarrays having bitwise XOR of all elements equals to B.

**Problem Constraints**

1 <= length of the array <= 105

1 <= A[i], B <= 109

**Input Format**

The first argument given is the integer array A.
 The second argument given is integer B.

**Output Format**

Return the total number of subarrays having bitwise XOR equals to B.

**Example Input**

Input 1:

```
 A = [4, 2, 2, 6, 4]
 B = 6
```

Input 2:

```
 A = [5, 6, 7, 8, 9]
 B = 5
```

**Example Output**

**Example Explanation**

Explanation 1:

```
 The subarrays having XOR of their elements as 6 are:
 [4, 2], [4, 2, 2, 6, 4], [2, 2, 6], [6]
```

Explanation 2:

```
 The subarrays having XOR of their elements as 5 are [5] and [5, 6, 7, 8, 9]
```

![Subarray%20with%20given%20XOR%20Interviewbit%2023eef2c0463a49d39f82740c705f99c1/superman.e804d3.png](Subarray%20with%20given%20XOR%20Interviewbit%2023eef2c0463a49d39f82740c705f99c1/superman.e804d3.png)

```cpp
int Solution::solve(vector<int> &A, int B) {
    // Answer variable
    int count = 0;
    int xorr = 0;
    map<int, int> freq;
    for(int i = 0; i<A.size(); i++){
        xorr = xorr^A[i]; // Taking prefix xor
        if(xorr == B) {
            count++; // if vaue of xor is equal to the target element the increament the count by 1
                     // note in this case the subarray will start from index 0
        }
        if(freq.find(xorr^B) != freq.end()){ // check whether the xorr^k is present in the map
            count += freq[xorr^B]; // If it is present in the map then that means that 
                                   //there are some arrays which are not starting from index 0 which
                                   // have has xorr equal to target
            
        }
        freq[xorr] += 1; 
    }
    return count;
}
```