# Sort array with squares! | Interviewbit

Created: May 10, 2022 2:16 AM
Tags: Arrays
URL: https://www.interviewbit.com/problems/sort-array-with-squares/submissions/

![Sort%20array%20with%20squares!%20Interviewbit%2049103fc6b186484f8c83bd6b0cb48aa8/cover.9f999f.svg](Sort%20array%20with%20squares!%20Interviewbit%2049103fc6b186484f8c83bd6b0cb48aa8/cover.9f999f.svg)

```cpp
vector<int> Solution::solve(vector<int> &A) {
    int count = 0;
    int d = A.size();
    vector<int> ans(d);
    for(int i=0; i<A.size(); i++){
        if(A[i]>=0){
            break;
        }
        else{
            A[i] = -A[i];
            count += 1;
        }
    }

    vector<int> a(count);
    for(int i=count -1 ; i>=0; i--){
        a[i] = A[count-i-1];
    }

    // Code for Merge Sort:
    int a1 = 0;
    int b = count;
    for(int i=0; i<d; i++){
        if(a[a1] >= A[b] && b < d){
            ans[i] = A[b];
            b+=1;
        }
        else if(a[a1] <= A[b] && a1 < count){
            ans[i] = a[a1];
            a1 += 1;
        }
        else if(b==d){
            ans[i]=a[a1];
            a1++;
        }
        else if(a1==count){
            ans[i] = A[b];
            b++;
        }
    }
    for(int i=0; i<ans.size(); i++){
        ans[i] = ans[i]*ans[i];
    }
    return ans;
}
```