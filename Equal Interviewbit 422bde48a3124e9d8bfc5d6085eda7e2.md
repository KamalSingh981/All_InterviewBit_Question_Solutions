# Equal | Interviewbit

Created: July 16, 2022 1:33 AM
Tags: Hashing
URL: https://www.interviewbit.com/problems/equal/

Given an array A of integers, find the index of values that satisfy `A + B = C + D`, where `A,B,C & D` are integers values in the array

**Note:**

```
1) Return the indices `A1 B1 C1 D1`, so that
  A[A1] + A[B1] = A[C1] + A[D1]
  A1 < B1, C1 < D1
  A1 < C1, B1 != D1, B1 != C1

2) If there are more than one solutions,
   then return the tuple of values which are lexicographical smallest.

Assume we have two solutions
S1 : A1 B1 C1 D1 ( these are values of indices int the array )
S2 : A2 B2 C2 D2

S1 is lexicographically smaller than S2 iff
  A1 < A2 OR
  A1 = A2 AND B1 < B2 OR
  A1 = A2 AND B1 = B2 AND C1 < C2 OR
  A1 = A2 AND B1 = B2 AND C1 = C2 AND D1 < D2

```

**Example:**

```
Input: [3, 4, 7, 1, 2, 9, 8]
Output: [0, 2, 3, 5] (O index)

```

If no solution is possible, return an empty list.

```cpp
bool canreplace(vector<int> a, vector<int> b){
    for(int i =0; i<4; i++){
        if(b[i]<a[i]) return true;
        else if(b[i] > a[i]) return false;
    }
    return false;
}
vector<int> Solution::equal(vector<int> &A) {
    unordered_map<int, pair<int,int>> m;
    int n = A.size();
    vector<int> ans = {n,0,0,0};
    for(int i = 0; i<A.size(); i++){
        for(int j = i + 1; j<A.size(); j++){
            int sum = A[i] + A[j];
            if(m.find(sum) !=m.end()){
                int idx1 = m[sum].first;
                int idx2 = m[sum].second;
                if(idx1 < i and idx2 != i and idx2 != j){
                    vector<int> temp = {idx1, idx2, i, j};
                    if(canreplace(ans, temp)){
                        ans = temp;
                    }
                }
            }
            else{
                m[sum] = {i,j};
            }
        }
    }
    if(ans[1] == 0) return {};
    return ans;
}
```