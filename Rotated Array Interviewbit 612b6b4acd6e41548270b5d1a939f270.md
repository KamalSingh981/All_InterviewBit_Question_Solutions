# Rotated Array | Interviewbit

Created: May 25, 2022 11:11 AM
Tags: Binary Search
URL: https://www.interviewbit.com/problems/rotated-array/

Suppose a sorted array A is rotated at some pivot unknown to you beforehand.

*(i.e., `0 1 2 4 5 6 7` might become `4 5 6 7 0 1 2`)*.

Find the minimum element.

The array will not contain duplicates.

> 
> 
> - **NOTE 1:** Also think about the case when there are duplicates. Does your current solution work? How does the time complexity change?*

**PROBLEM APPROACH:**

**Note:** If you know the number of times the array is rotated, then this problem becomes trivial. If the number of rotation is x, then minimum element is A[x].
 Lets look at how we can calculate the number of times the array is rotated.

Complete solution in the hints.

```cpp
int Solution::findMin(const vector<int> &A) 
{
    int n=A.size();
int low=0; int high=n-1; int index=0; //index of a small number
while(low<=high)
{
int mid = (low+high)/2;
if(A[mid]<A[index]) //as the array sorted search on left until finding small number
{
index=mid;
high = mid-1;
}
else{ low=mid+1; } //else search on right
}
return A[index]; 

}
```