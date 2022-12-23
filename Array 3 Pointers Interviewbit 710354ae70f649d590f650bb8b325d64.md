# Array 3 Pointers | Interviewbit

Created: June 14, 2022 12:21 AM
Tags: Two pointers
URL: https://www.interviewbit.com/problems/array-3-pointers/

You are given 3 arrays A, B and C. All 3 of the arrays are sorted.

Find `i, j, k` such that :`max(abs(A[i] - B[j]), abs(B[j] - C[k]), abs(C[k] - A[i]))` is minimized.
 Return the minimum `max(abs(A[i] - B[j]), abs(B[j] - C[k]), abs(C[k] - A[i]))`

- *abs(x) is absolute value of x and is implemented in the following manner : **

```
      if (x < 0) return -x;
      else return x;

```

**Example :**

```
Input :
        A : [1, 4, 10]
        B : [2, 15, 20]
        C : [10, 12]

Output : 5
         With 10 from A, 15 from B and 10 from C.

```

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
bool comp(int a, int b)
{
 return (a < b);
}
int Solution::minimize(const vector<int> &A, const vector<int> &B, const vector<int> &C) {
    int i = 0, j = 0, k = 0;
    int ans = INT_MAX;
    while(i<A.size() && j<B.size() && k<C.size()){
        ans = min(ans, max({abs(A[i] - B[j]), abs(B[j] - C[k]), abs(C[k]- A[i])}, comp));
        if(A[i] <= B[j] && A[i]<= C[k]){
            i++;
        }
        else if(B[j]<=A[i] && B[j]<= C[k]){
            j++;
        }
        else{
            k++;
        }
    }
    return ans;
}
```