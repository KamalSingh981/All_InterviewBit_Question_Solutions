# Median of Array | Interviewbit

Created: June 18, 2022 5:17 PM
Tags: Binary Search
URL: https://www.interviewbit.com/problems/median-of-array/

There are two sorted arrays A and B of size m and n respectively.

Find the median of the two sorted arrays ( The median of the array formed by merging both the arrays ).

The overall run time complexity should be `O(log (m+n))`.

**Sample Input**

```
A : [1 4 5]
B : [2 3]

```

**Sample Output**

```
3

```

> 
> 
> 
> NOTE: IF the number of elements in the merged array is even, then the median is the average of n / 2 th and n/2 + 1th element.  For example, if the array is [1 2 3 4], the median is (2 + 3) / 2.0 = 2.5
> 

```cpp
double Solution::findMedianSortedArrays(const vector<int> &A, const vector<int> &B) {
int lo=INT_MAX,hi=INT_MIN;
    vector<int>med(2);
    //finding max,min
    int n=A.size(),m=B.size();
    if(A.size() > 0){
    lo = A[0],hi=A[n-1];
    }
    if(B.size() > 0){
        lo = min(lo,B[0]);
        hi = max(hi,B[m-1]);
    }
//finding median indices
    if((n+m)%2 == 0){
        med[0] = (n+m)/2;
        med[1] = med[0]+1;
    }
    else med[0] = med[1] = (n+m+1)/2;

    double median = 0;
    for(int i=0;i<2;i++){
        int low = lo,high=hi,mid;
        while(low<high){
            int cnt = 0;
            mid = low+(high-low)/2;
            if(n > 0) cnt += upper_bound(A.begin(),A.end(),mid)-A.begin();
            if(m > 0) cnt += upper_bound(B.begin(),B.end(),mid)-B.begin();
            if(cnt >= med[i]){
                high = mid;
            }
            else{
                low = mid+1;
            }
        }
        median += low;
        if((n+m)%2 == 1) return median;
    }
    return (double)(median/2.0);
}
```