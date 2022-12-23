# Stepping Numbers | Interviewbit

Created: July 29, 2022 12:44 PM
Tags: DFS, Graphs
URL: https://www.interviewbit.com/problems/stepping-numbers/

**Problem Description**

Given **A** and **B** you have to find all stepping numbers in range **A** to **B**.

**The stepping number:**

A number is called as a stepping number if the adjacent digits have a difference of 1.

e.g. 123 is stepping number, but 358 is not a stepping number

**Input Format**

First argument is an integer **A**.

Second argument is an integer **B**.

**Output Format**

Return a integer array sorted in ascending order denoting the stepping numbers between **A** and **B**.

**Example Input**

**Example Output**

**Example Explanation**

```cpp
void dfs(int i, int A, int B, vector<int> &ans){
    if(i>=A and i<=B){
        ans.push_back(i);
    }
    if(i == 0  || i>B){
        return;
    }
    
    
    int last = i%10;
    if(last != 0){
        dfs(i*10 + last - 1, A, B, ans);
    }
    if(last != 9){
        dfs(i*10 + last + 1, A, B, ans);
    }
    
}
vector<int> Solution::stepnum(int A, int B) {
    
    vector<int> ans;
    for(int i = 0; i<10; i++){
        dfs(i, A, B, ans);
    }
    sort(ans.begin(), ans.end());
    return ans;
}
```

Linear time complexity

```cpp
bool isstep(int i){
    
    int n = i%10;
    i /= 10;
    while(i!=0){
        if(abs(n - i%10) != 1){
            return false;
        }
        n = i%10;
        i /= 10;
    }
    
    return true;
}
vector<int> Solution::stepnum(int A, int B) {
    
    vector<int> ans;
    for(int i = A; i<=B; i++){
        if(isstep(i)){
            ans.push_back(i);
        }
    }
    return ans;
}
```