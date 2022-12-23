# First Missing Integer | Interviewbit

Created: May 15, 2022 12:46 PM
URL: https://www.interviewbit.com/problems/first-missing-integer/

Given an unsorted integer array, find the first missing positive integer.

**Example:**

Given `[1,2,0]` return 3,

`[3,4,-1,1]` return 2,

`[-8, -7, -6]` returns 1

Your algorithm should run in `O(n)` time and use constant space.

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
int fingmissingpositive(vector<int> a, int size){
    bool present[size+1] = {false};
    int i;
    int count = 0;
    for(i = 0; i<size; i++){
        if(a[i]>0&& a[i]<=size){
            present[a[i]] = true;
        }
        else if(a[i]<0){
            count += 1;
        }
    }

    for(i = 1; i<size; i++){
        if(!present[i]){
            return i;
        }
    }
    if(count == size){
        return 1;
    }
    return size + 1;
}
int Solution::firstMissingPositive(vector<int> &A) {

        return fingmissingpositive(A, A.size());

}
```

### Interview bit Code

```cpp
int Solution::firstMissingPositive(vector<int> &A) {
    int n = A.size();
    for(int i = 0; i<n; i++){
        if(A[i]>0 && A[i]<=n){
            int pos = A[i] -1;
            if(A[pos] != A[i]){
                swap(A[pos], A[i]);
                i--;
            }    
        }
    }
    for(int i = 0; i<n; i++){
        if(A[i] != i+1){
            return i+1;
        }
    }
    return n + 1;

}
```

# Algorithm

We traverse the array and if A[i] is in [1,N] range, we try to put in the index of same value in the array.