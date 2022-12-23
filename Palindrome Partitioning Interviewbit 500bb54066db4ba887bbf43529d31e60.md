# Palindrome Partitioning | Interviewbit

Created: July 14, 2022 2:34 AM
Tags: Backtracking, Recursion
URL: https://www.interviewbit.com/problems/palindrome-partitioning/

Given a string s, partition s such that every string of the partition is a palindrome.

Return all possible palindrome partitioning of s.

For example, given `s = "aab"`,
 Return

```
  [
    ["a","a","b"]
    ["aa","b"],
  ]

```

> 
> 
> 
> **Ordering the results in the answer :**
> 
> Entry i will come before Entry j if :
> 
> - len(Entryi[0]) < len(Entryj[0]) OR
> - (len(Entryi[0]) == len(Entryj[0]) AND len(Entryi[1]) < len(Entryj[1])) OR * * *
> - (len(Entryi[0]) == len(Entryj[0]) AND … len(Entryi[k] < len(Entryj[k]))

In the given example,`["a", "a", "b"]` comes before `["aa", "b"]` because `len("a") < len("aa")`

```cpp
bool ispalindrome(string s){
    int  n = s.length();
    for(int i = 0; i<n/2; i++){
        if(s[i] !=  s[n - i -1]){
            return false;
        }
    }
    
    return true;
}
void findallthepalindrome(string A, vector<vector<string>> &ans, vector<string> a, int i){
    // Base Case
    if(i == A.length()){
        ans.push_back(a);
        return;
    }
    
    // Recursive Case
    for(int j = i; j<A.length(); j++){
        string q = A.substr(i, j -i+1);
        if(ispalindrome(q)){
            a.push_back(q);
            findallthepalindrome(A, ans, a, j+1);
            a.pop_back();
        }
    }
    
}

vector<vector<string> > Solution::partition(string A) {
    // Do not write main() function.
    // Do not read input, instead use the arguments to the function.
    // Do not print the output, instead return values as specified
    // Still have a doubt. Checkout www.interviewbit.com/pages/sample_codes/ for more details
    vector<vector<string>> ans;
    vector<string> a;
    findallthepalindrome(A, ans, a, 0);
    return ans;
}
```