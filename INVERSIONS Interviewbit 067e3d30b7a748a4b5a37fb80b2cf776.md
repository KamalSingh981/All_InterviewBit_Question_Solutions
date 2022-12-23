# INVERSIONS | Interviewbit

Created: August 10, 2022 11:52 AM
Tags: Arrays, Sorting
URL: https://www.interviewbit.com/problems/inversions/

Given an array A, count the number of inversions in the array.

Formally speaking, two elements `A[i]` and `A[j]` form an inversion if `A[i] > A[j]` and `i < j`

**Example:**

```
A : [2, 4, 1, 3, 5]
Output : 3

```

as the 3 inversions are `(2, 1), (4, 1), (4, 3)`.

```cpp
long long merge(long long arr[], int left, int mid, int right) {
  int i = left, j = mid, k = 0;
  long long invCount = 0;
  int temp[(right - left + 1)];
 
  while ((i < mid) && (j <= right)) {
    if (arr[i] <= arr[j]) {
      temp[k] = arr[i];
      ++k;
      ++i;
    } else {
      temp[k] = arr[j];
      invCount += (mid - i);
      ++k;
      ++j;
    }
  }
 
  while (i < mid) {
    temp[k] = arr[i];
    ++k;
    ++i;
  }
 
  while (j <= right) {
    temp[k] = arr[j];
    ++k;
    ++j;
  }
 
  for (i = left, k = 0; i <= right; i++, k++) {
    arr[i] = temp[k];
  }
 
  return invCount;
}
long long mergeSort(long long arr[], int left, int right) {
  long long invCount = 0;
 
  if (right > left) {
    int mid = (right + left) / 2;
    invCount = mergeSort(arr, left, mid);
    invCount += mergeSort(arr, mid + 1, right);
    invCount += merge(arr, left, mid + 1, right);
  }
  return invCount;
}

int Solution::countInversions(vector<int> &A) {
    
    
    long long arr[A.size()];
    for(int i = 0; i<A.size(); i++){
        arr[i] = A[i];
    }
    return mergeSort(arr, 0, A.size() - 1);
}
```