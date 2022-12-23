# 3 Sum | Interviewbit

Created: June 13, 2022 2:30 PM
Tags: Two pointers
URL: https://www.interviewbit.com/problems/3-sum/

Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. 
 Return the sum of the three integers.

*Assume that there will only be one solution*

**Example:** 
 given array `S = {-1 2 1 -4}`, 
 and `target = 1`.

The sum that is closest to the target is `2`. `(-1 + 2 + 1 = 2)`

```cpp
int Solution::threeSumClosest(vector<int> &A, int B) {
    if(A.size()<3){
        return 0;
    }

    sort(A.begin(), A.end());
    int ans;
    int a = abs(A[0] + A[1] + A[A.size()-1] - B);

    for(int i = 0; i<A.size() - 2; i++){
        if(i>0 && A[i] == A[i-1]){
            continue;
        }
        int start = i+1;
        int end = A.size()-1;
        while(start < end){
            int temp = A[i] + A[start] + A[end] - B;
            if(abs(temp) <= abs(a)){
                ans = (int)temp + B;
                a = temp;
            }
            if(temp == 0){
                return ans;
            }
            else if(temp>0){
                end--;
            }
            else{
                start++;
            }
        }
    }
    return ans;
}
```

Algorithm is same as done in [https://www.interviewbit.com/problems/3-sum-zero/](https://www.interviewbit.com/problems/3-sum-zero/).

```cpp
int Solution::nTriang(vector<int> &A) {
    sort(A.begin(), A.end());
    long long ans = 0;
    int mod = 1000000007;
    int n = A.size();
    for(int i = n - 1; i>= 2; i--){
        int st = 0;
        int en = i - 1;
        while(st<en){
            if(A[st] + A[en] > A[i]){
                ans += (en - st)%mod;
                en--;
            }
            else{
                st++;
            }
        }
    } 
    return ans%mod;
}
```