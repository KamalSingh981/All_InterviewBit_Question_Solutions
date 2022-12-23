# Maximum Absolute Difference | Interviewbit

Created: May 15, 2022 5:11 PM
URL: https://www.interviewbit.com/problems/maximum-absolute-difference/

You are given an array of N integers, A1, A2 ,…, AN. Return maximum value of `f(i, j)` for all 1 ≤ *i, j* ≤ N.`f(i, j)` is defined as `|A[i] - A[j]| + |i - j|`, where |x| denotes absolute value of x.

**For example**,

```
A=[1, 3, -1]

f(1, 1) = f(2, 2) = f(3, 3) = 0
f(1, 2) = f(2, 1) = |1 - 3| + |1 - 2| = 3
f(1, 3) = f(3, 1) = |1 - (-1)| + |1 - 3| = 4
f(2, 3) = f(3, 2) = |3 - (-1)| + |2 - 3| = 5

So, we return 5.

```

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp

int maxDistance(vector<int> A, int n){
    int max1 = INT_MIN, min1 = INT_MAX;
    int max2 = INT_MIN, min2 = INT_MAX;

    for(int i =0; i<n; i++){
        max1 = max(max1, A[i]+i);
        min1 = min(min1, A[i]+i);
        max2 = max(max2, A[i]-i);
        min2 = min(min2, A[i]-i);

    }
    return max(max1- min1, max2 - min2);
}
int Solution::maxArr(vector<int> &A) {
int n = A.size();
return maxDistance(A, n);
}
```

### Algorithm is based on the results obtained from manipulating the given the equation.

![Untitled](Maximum%20Absolute%20Difference%20Interviewbit%20e7ec9c043e6d43e2a0ede25a30a75579/Untitled.png)

`f(i, j) = |A[i] - A[j]| + |i - j|` can be written in 4 ways (Since we are looking at max value, we don’t even care if the value becomes negative as long as we are also covering the max value in some way).

`(A[i] + i) - (A[j] + j)
-(A[i] - i) + (A[j] - j) 
(A[i] - i) - (A[j] - j) 
(-A[i] - i) + (A[j] + j) = -(A[i] + i) + (A[j] + j)`

Note that case 1 and 4 are equivalent and so are case 2 and 3.

We can construct two arrays with values: `A[i] + i` and `A[i] - i`. Then, for above 2 cases, we find the maximum value possible. For that, we just have to store minimum and maximum values of expressions `A[i] + i` and `A[i] - i` for all `i`.