# Search in Bitonic Array! | Interviewbit

Created: May 13, 2022 4:01 PM
URL: https://www.interviewbit.com/problems/search-in-bitonic-array/

**Problem Description**

Given a bitonic sequence **A** of **N** distinct elements, write a program to find a given element **B** in the bitonic sequence in **O(logN)** time.

**NOTE:**

- A Bitonic Sequence is a sequence of numbers which is first strictly increasing then after a point strictly decreasing.

**Problem Constraints**

3 <= N <= 105

1 <= A[i], B <= 108

Given array always contain a bitonic point.

Array A always contain distinct elements.

**Input Format**

First argument is an integer array **A** denoting the bitonic sequence.

Second argument is an integer **B**.

**Output Format**

Return a single integer denoting the position (0 index based) of the element **B** in the array **A** if **B** doesn't exist in **A** return **-1**.

**Example Input**

Input 1:

```
 A = [3, 9, 10, 20, 17, 5, 1]
 B = 20

```

Input 2:

```
 A = [5, 6, 7, 8, 9, 10, 3, 2, 1]
 B = 30

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 B = 20 present in A at index 3

```

Explanation 2:

```
 B = 30 is not present in A

```

```cpp
int  findmax(vector<int> arr, int low, int high){
    if(low== high){
        return arr[low];
    }
    if((high == low +1) && arr[low] >= arr[high])
        return arr[low];

    if((high == low +1)&& arr[low] < arr[high]){
        return arr[high];
    }

    int mid = (low + high)/ 2;

    if(arr[mid] > arr[mid+1] && arr[mid] > arr[mid+1]){
        return mid;
    }
    if(arr[mid] > arr[mid+1]&& arr[mid] < arr[mid-1]){
        return findmax(arr, low, mid-1);
    }
    else{
        return findmax(arr, mid +1, high);
    }
}

int ascendingBinarysearch(vector<int> &arr, int low, int high, int key)
{
    while(low<=high){
        int mid = low + (high - low)/2;
        if(arr[mid] == key){
            return mid;
        }
        if (arr[mid] > key){
            high = mid - 1;
        }
        else{
            low = mid +1;
        }
    }
    return -1;
}

// Function for binary search in descending part of array
int descendingBinaryseach(vector<int> &arr, int low, int high, int key){
    while (low<= high){
        int mid = low + (high - low)/2;
        if (arr[mid] == key)
            return mid;
        if (arr[mid] < key)
            high = mid - 1;
        else
            low = mid +1;
    }
    return -1;
}

int searchBitonic(vector<int> &arr, int n, int key, int index){
    if (key > arr[index])
        return -1;
    else if(key == arr[index]){
        return index;
    }
    else{
        int temp = ascendingBinarysearch(arr, 0, index-1, key);
        if (temp != -1){
            return temp;
        }

        return descendingBinaryseach(arr,index+1, n-1, key);
    }
}

int Solution::solve(vector<int> &A, int B) {
    int index = findmax(A, 0,A.size()-1);
    int x = searchBitonic(A, A.size(),B, index);
    if(x == -1)
        return -1;
    else
        return x;
}
```