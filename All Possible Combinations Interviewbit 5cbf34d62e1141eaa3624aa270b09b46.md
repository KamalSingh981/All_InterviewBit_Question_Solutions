# All Possible Combinations | Interviewbit

Created: July 14, 2022 1:53 AM
Tags: Backtracking, Recursion
URL: https://www.interviewbit.com/problems/all-possible-combinations/

**Problem Description**

You are given a array of strings **A** of length **N**.

You have to return another string array which contains all possible special strings.
 A special string is defined as a string with length equal to N, 
 and ith character of the string is equal to any character of the ith string in the array A.

**Problem Constraints**

**Input Format**

**Output Format**

**Example Input**

Input 1:

```
A = ['ab', 'cd']

```

Input 2:

```
A = ['aa', 'bb']

```

**Example Output**

Output 1:

```
['ac', 'ad', 'bc', 'bd']

```

Output 2:

```
['ab', 'ab', 'ab', 'ab']

```

**Example Explanation**

Explanation 1:

```
Since, the first character has to be from the 1st string 'ab' and the 2nd from 'cd'.
These are the all possible 4 combinations.
```

Explanation 2:

```
Note we can have duplicate strings, you have to add all of them.

```

```cpp
void findCombinations(vector<string> A, vector<string> &ans, int  i, string a){
    // Base Case
    if(i == A.size()){
        ans.push_back(a);
        return;
    }
    
    // Recursive Case
    string t = A[i];
    for(int k = 0; k<t.size(); k++){
        a.push_back(A[i][k]);
        findCombinations(A, ans, i + 1, a);
        a.pop_back();
    }
}

vector<string> Solution::specialStrings(vector<string> &A) {
   vector<string> ans;
   findCombinations(A, ans,0, "");
   return ans;
}
```