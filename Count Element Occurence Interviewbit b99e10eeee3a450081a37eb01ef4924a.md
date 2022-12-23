# Count Element Occurence | Interviewbit

Created: May 23, 2022 12:24 AM
Tags: Binary Search
URL: https://www.interviewbit.com/problems/count-element-occurence/

Given a sorted array of integers, find the number of occurrences of a given target value.
 Your algorithm’s runtime complexity must be in the order of `O(log n)`.
 If the target is not found in the array, **return `0`**

- *Example : ** Given `[5, 7, 7, 8, 8, 10]` and target value 8, return 2.

PROBLEM APPROACH :

For complete solution, look at the hint.

```cpp
int Solution::findCount(const vector<int> &A, int B) {
    int l = 0;
    int r = A.size() -1;
    int mid = l + r/2;
    int index = -1;
    while(l<=r){
        mid = l + (r-l)/2;
        if(A[mid] == B){
            index = mid;
            break;
        }
        else if(A[mid]<B){
            l = mid+1;
        }
        else{
            r = mid-1;
        }
    }
    if(index == -1){
        return 0;
    }
    int ans = 1;
    int left = mid - 1;
    int right = mid + 1;
    while (left>=0 && A[left] == B){
        ans++;
        left--;
    }
    while(right<A.size() && A[right] == B){
        ans++;
        right++;
    }
    return ans;
}
```