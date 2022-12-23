# Points on the Straight Line | Interviewbit

Created: July 16, 2022 8:46 PM
Tags: Hashing
URL: https://www.interviewbit.com/problems/points-on-the-straight-line/

Given n points on a 2D plane, find the maximum number of points that lie on the same straight line.

Sample Input :

```
(1, 1)
(2, 2)

```

Sample Output :

```
2

```

You will be given 2 arrays `X` and `Y`. Each point is represented by `(X[i], Y[i])`

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
int Solution::maxPoints(vector<int> &A, vector<int> &B) {
    int ans  = 1;
    if(A.size() == 0){ // Edge Case
        return 0;
    }
    for(int i = 0; i<A.size(); i++){
        unordered_map<double, int> m;
        for(int j = 0; j<B.size(); j++){
            if(i == j){ // if the point is same then we will not add slop to the map
                continue;
            }
            double x1 = A[i], x2 = A[j], y1 = B[i], y2 = B[j];
            if(A[i] == A[j]){      // if the line is parallel to the y axis then adding  to the map
                m[INT_MAX]++;
            }
            else{
                double t = (y1 - y2) / (x1 - x2); // Adding the slop the map
                m[t]++;
            }
        }
        for(auto s:m){
        ans = max(ans, s.second+1);
    }
    }
    
    return ans;
}
```