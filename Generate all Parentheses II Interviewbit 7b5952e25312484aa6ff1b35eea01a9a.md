# Generate all Parentheses II | Interviewbit

Created: July 14, 2022 3:13 AM
Tags: Backtracking, Recursion
URL: https://www.interviewbit.com/problems/generate-all-parentheses-ii/

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses of length `2*n`.

For example, given `n = 3`, a solution set is:

Make sure the returned list of strings are sorted.

```cpp
void findallparentheses(int A, int B, vector<string> &ans, string s){
    // Base Case
    if(A <= 0 && B <= 0){
        ans.push_back(s);
        return;
    }
    if(A < 0  || B < 0 ){
        return;
    }
    
    // Recursive Case
    s += '(';
    findallparentheses(A - 1, B, ans, s);
    s.pop_back();
    if(A<B){
        s += ')';
        findallparentheses(A, B-1, ans, s);
        s.pop_back();    
    }
}

vector<string> Solution::generateParenthesis(int A) {
    vector<string> ans;
    findallparentheses(A, A, ans, "");
    return ans;
}
```