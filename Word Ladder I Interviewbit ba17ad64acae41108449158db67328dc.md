# Word Ladder I | Interviewbit

Created: July 29, 2022 7:37 PM
Tags: Graphs
URL: https://www.interviewbit.com/problems/word-ladder-i/

Given two words **A** and **B**, and a dictionary, **C**, find the length of **shortest** transformation sequence from **A** to **B**, such that:

- You must change exactly **one** character in every transformation.
- Each intermediate word must exist in the dictionary.

**Note:**

1. Return **0** if there is no such transformation sequence.
2. All words have the same length.
3. All words contain only lowercase alphabetic characters.

**Input Format:**

```
The first argument of input contains a string, A.
The second argument of input contains a string, B.
The third argument of input contains an array of strings, C.

```

**Output Format:**

```
Return an integer representing the minimum number of steps required to change string A to string B.

```

**Constraints:**

```
1 <= length(A), length(B), length(C[i]) <= 25
1 <= length(C) <= 5e3

```

**Example :**

```
Input 1:
    A = "hit"
    B = "cog"
    C = ["hot", "dot", "dog", "lot", "log"]

Output 1:
    5

Explanation 1:
    "hit" -> "hot" -> "dot" -> "dog" -> "cog"

```

```cpp
int Solution::solve(string A, string B, vector<string> &C) {
    
    map<string, vector<string>> m;
    int stringsize = A.length();
        
    for(int i = 0; i<C.size(); i++){
        string str = C[i];
        for(int j = 0; j<stringsize; j++){
            string s = str.substr(0, j) + "*" + str.substr(j+1, stringsize - j-1);
            m[s].push_back(str);
        }
    }
    
    
    string str = A;
    for(int i =0; i<stringsize; i++){
        string s = str.substr(0, i) + "*" + str.substr(i+1, stringsize - i-1);
        m[s].push_back(str);
    }
    
    queue<pair<string, int>> q;
    q.push({A, 1});
    set<string> visited;
    visited.insert(A);
    
    while(!q.empty()){
        string str = q.front().first;
        int level = q.front().second;
        q.pop();
        for(int i = 0; i<stringsize; i++){
            string p = str.substr(0, i) + "*" + str.substr(i+1, stringsize - i -1);
            vector<string> v = m[p];
            
            for(string x:v){
                if(visited.find(x) == visited.end()){
                    q.push({x, level+1});
                    visited.insert(x);
                    
                    if(x == B) return level +1;
                }
            }
        }
        
        
    }
    return 0;
}
```