# Simple bactracking - Community Discussions | Interviewbit

Created: July 12, 2022 9:48 PM
Tags: Backtracking, Recursion
URL: https://www.interviewbit.com/problems/combination-sum-ii/discussion/p/simple-bactracking/287109/651

void solve(int ind,vector<int>&A,vector<vector<int>>&ans,vector<int>&res,int k){

if(k==0){

ans.push_back(res);

for(int i=ind;i<A.size();i++){

if(i!=ind&&A[i]==A[i-1])continue;

if(A[i]<=k){

res.push_back(A[i]);

solve(i+1,A,ans,res,k-A[i]);

res.pop_back();

vector<vector<int> > Solution::combinationSum(vector<int> &A, int B) {

vector<vector<int>>ans;

vector<int>res;

sort(A.begin(),A.end());

solve(0,A,ans,res,B);

return ans;

```cpp
void combinationalSum(int index, vector<int> A, int B, vector<vector<int>> &ans, vector<int> a){
    // Base Case
    if(B == 0){
        ans.push_back(a);
        return;
    }
    
    // Recursive Case
    for(int i = index; i<A.size(); i++){
        if(i!=index &&A[i] == A[i-1]) continue;
        if(A[i] <=B){
            a.push_back(A[i]);
            combinationalSum(i +1, A, B - A[i], ans, a);
            a.pop_back();
        }
    }
}

vector<vector<int> > Solution::combinationSum(vector<int> &A, int B) {
    // Do not write main() function.
    // Do not read input, instead use the arguments to the function.
    // Do not print the output, instead return values as specified
    // Still have a doubt. Checkout www.interviewbit.com/pages/sample_codes/ for more details
    sort(A.begin(), A.end());
    vector<vector<int>> ans;
    vector<int> a;
    combinationalSum(0, A, B, ans, a);
    return ans;
}
```