# Pangram Check | Interviewbit

Created: May 9, 2022 1:55 AM
URL: https://www.interviewbit.com/problems/pangram-check/

**Problem Description**

Given a sentence represented as an array **A** of strings.
Chech if it is a **pangram** or not.
A pangram is a unique sentence in which every letter of the alphabet is used at least once.

**Problem Constraints**

**Input Format**

**Output Format**

**Example Input**

Input 1:

```
A = ["the", "quick", "brown", "fox", "jumps", "over", "the", "lazy", "dog"]

```

Input 2:

```
A = ["interviewbit", "scaler"]

```

**Example Output**

**Example Explanation**

Explanation 1:

```
We can check that all english alphabets are present in given sentence.

```

Explanation 2:

```
Not all english alphabets are present.

```

```cpp
#include <iostream>
#include <cctype>
#include <iterator>
#include <set>
using namespace std;
int Solution::solve(vector<string> &A) {
    string a = "";
    for(int i=0; i<A.size(); i++){
        a+=A[i];
    }
    set<char> s1;
    for(int i=0; i<a.length(); i++){
        s1.insert(tolower(a[i]));
    }

    if (s1.size() !=26){
        return 0;
    }
    else{
        return 1;
    }
    
}
```