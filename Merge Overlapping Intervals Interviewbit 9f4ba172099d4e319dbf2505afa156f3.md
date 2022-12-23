# Merge Overlapping Intervals | Interviewbit

Created: May 14, 2022 10:27 PM
URL: https://www.interviewbit.com/problems/merge-overlapping-intervals/

Given a collection of intervals, merge all overlapping intervals.

**For example:**

Given `[1,3],[2,6],[8,10],[15,18]`,

return `[1,6],[8,10],[15,18]`.

Make sure the returned intervals are sorted.

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

# My code

```cpp
/**
 * Definition for an interval.
 * struct Interval {
 *     int start;
 *     int end;
 *     Interval() : start(0), end(0) {}
 *     Interval(int s, int e) : start(s), end(e) {}
 * };
 */
bool compareInterval(Interval i1, Interval i2)
{
    return (i1.start < i2.start);
}
vector<Interval> Solution::merge(vector<Interval> &A) {
    // Do not write main() function.
    // Do not read input, instead use the arguments to the function.
    // Do not print the output, instead return values as specified
    // Still have a doubt. Checkout www.interviewbit.com/pages/sample_codes/ for more details
    int n = A.size();
    sort(A.begin(),A.end(), compareInterval);
    vector<Interval> ans; 
    bool flag = true;
    int a= A[0].start;
    int b = A[0].end;
    for(int i = 0; i<n-1; i++){
        if (b>=A[i+1].start){
            b = max(b,A[i+1].end);
            flag = true;
            continue;
        }
        else{
            ans.push_back({a,b});
            a = A[i+1].start;
            b = A[i+1].end;
            flag = false;
        }
    }
    if(flag){
        ans.push_back({a,b});
    }
    int q = ans.size();
    if(A[n-1].start>ans[q-1].end){
        a = A[n-1].start;
        b = A[n-1].end;
        ans.push_back({a,b});
    }
    return ans;
}
```

# Interview Bit Code

```cpp
/**
 * Definition for an interval.
 * struct Interval {
 *     int start;
 *     int end;
 *     Interval() : start(0), end(0) {}
 *     Interval(int s, int e) : start(s), end(e) {}
 * };
 */
bool compareInterval(Interval i1, Interval i2)
{
    return (i1.start < i2.start);
}
vector<Interval> Solution::merge(vector<Interval> &A) {
    // Do not write main() function.
    // Do not read input, instead use the arguments to the function.
    // Do not print the output, instead return values as specified
    // Still have a doubt. Checkout www.interviewbit.com/pages/sample_codes/ for more details
    int n = A.size();
    sort(A.begin(),A.end(), compareInterval);
    vector<Interval> ans; 
    ans.push_back(A[0]);
    for(int i=1; i<A.size(); i++){
        if(A[i].start <= ans.back().end) ans.back().end = max(ans.back().end, A[i].end);
        else ans.push_back(A[i]);
    }
    return ans;
}
```