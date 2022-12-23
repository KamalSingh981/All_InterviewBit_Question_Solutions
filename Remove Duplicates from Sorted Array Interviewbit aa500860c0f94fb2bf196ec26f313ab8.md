# Remove Duplicates from Sorted Array | Interviewbit

Created: May 30, 2022 1:12 AM
Tags: Two pointers
URL: https://www.interviewbit.com/problems/remove-duplicates-from-sorted-array/

**Problem Description**

Given a sorted array **A** consisting of duplicate elements.

Your task is to remove all the duplicates and return a sorted array of distinct elements consisting of all distinct elements present in **A**.

But, instead of returning an answer array, you have to **rearrange the given array in-place** such that it resembles what has been described above. Hence, return a single integer, the index(1-based) till which the answer array would reside in the given array **A**.

**Note**: This integer is the same as the number of integers remaining inside **A** had we removed all the duplicates. Look at the example explanations for better understanding.

**Input Format**

First and only argurment containing the integer array A.

**Output Format**

**Example Input**

Input 1:

```
A = [1, 1, 2]
```

Input 2:

```
A = [1, 2, 2, 3, 3]
```

**Example Output**

**Example Explanation**

Explanation 1:

```
Updated Array: [1, 2, X] after rearranging. Note that there could be any number in place of x since we dont need it.
We return 2 here.
```

Explanation 2:

```
Updated Array: [1, 2, 3, X, X] after rearranging duplicates of 2 and 3.
We return 3 from here.
```

```cpp
int Solution::removeDuplicates(vector<int> &A) {
    int ans = 0;
    for(int i=1; i<A.size(); i++){
        if(A[i]!=A[ans]){
            ans++;
            A[ans] = A[i];      
        }
    }
    return ans+1;
}
```