# C solution easy to understand - Community Discussions | Interviewbit

Created: July 15, 2022 10:17 PM
Tags: Hashing
URL: https://www.interviewbit.com/problems/two-out-of-three/discussion/p/c-solution-easy-to-understand/299478/1963

vector<int> Solution::solve(vector<int> &A, vector<int> &B, vector<int> &C) {

map<int, unordered_set<int>> mp;

for(int i=0; i< A.size(); i++) mp[A[i]].insert(1);

for(int i=0; i< B.size(); i++) mp[B[i]].insert(2);

for(int i=0; i< C.size(); i++) mp[C[i]].insert(3);

vector<int> ans;

for(auto i: mp) {

if(i.second.size()>= 2) ans.push_back(i.first);

return ans;

```cpp
vector<int> Solution::solve(vector<int> &A, vector<int> &B, vector<int> &C) {
    map<int, unordered_set<int>> m;
    for(int i =0; i<A.size(); i++) m[A[i]].insert(1);
    for(int i =0; i<B.size(); i++) m[B[i]].insert(2);
    for(int i =0; i<C.size(); i++) m[C[i]].insert(3);
    
    vector<int> ans;
    for(auto i:m){
        if(i.second.size() >= 2){
            ans.push_back(i.first);
        }
    }
    return ans; 
}
```