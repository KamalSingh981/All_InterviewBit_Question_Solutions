# Majority Element | Interviewbit

Created: May 12, 2022 12:02 PM
URL: https://www.interviewbit.com/problems/majority-element/

Given an array of size **n**, find the majority element. The majority element is the element that appears more than **floor(n/2)** times.

You may assume that the array is non-empty and the majority element always exist in the array.

Example :

```
Input : [2, 1, 2]
Return  : 2 which occurs 2 times which is greater than 3/2.

```

```cpp
from collections import Counter
class Solution:
    # @param A : tuple of integers
    # @return an integer
    def majorityElement(self, A):
        d = Counter(A)
        cri = len(A)//2
        for i in d:
            if d.get(i)>cri:
                return i
```

Moore’ Voting Algorithm

- This is a two -step process.
- The first step gives the element that maybe the majority element in the array. If there is a majority element in an array, then this step will definitely return majority element, otherwise, it will return candidate for majority element.
- Check if the element obtained from the above steop is majority element. This step is necessary as there might be no majority element.
1. Algorithm
- Loop through each element and maintains a count of majority element, and a majority index maj_index
- if the next element is same then incremene thte count if the next elemetn is not same then decrement the count.
- if the count reaches 0 then changes the maj_index to the current element and set the count again to 1.
- Now again traves through the array and find the count of majority element found .
- The the count is greater than half the size of the array, print the element
- Else, print that there is no majority element.

```cpp
#include <bits/stdc++.h>
using namespace std;
 
/* Function to find the candidate for Majority */
int findCandidate(int a[], int size)
{
    int maj_index = 0, count = 1;
    for (int i = 1; i < size; i++) {
        if (a[maj_index] == a[i])
            count++;
        else
            count--;
        if (count == 0) {
            maj_index = i;
            count = 1;
        }
    }
    return a[maj_index];
}
 
/* Function to check if the candidate
   occurs more than n/2 times */
bool isMajority(int a[], int size, int cand)
{
    int count = 0;
    for (int i = 0; i < size; i++)
 
        if (a[i] == cand)
            count++;
 
    if (count > size / 2)
        return 1;
 
    else
        return 0;
}
 
/* Function to print Majority Element */
void printMajority(int a[], int size)
{
    /* Find the candidate for Majority*/
    int cand = findCandidate(a, size);
 
    /* Print the candidate if it is Majority*/
    if (isMajority(a, size, cand))
        cout << " " << cand << " ";
 
    else
        cout << "No Majority Element";
}
 
/* Driver code */
int main()
{
    int a[] = { 1, 3, 3, 1, 2 };
    int size = (sizeof(a)) / sizeof(a[0]);
 
    // Function calling
    printMajority(a, size);
 
    return 0;
}
```

Time complexity is O(n)

Auxiliary Space O(1)