# Word Break II | Interviewbit

Created: August 7, 2022 2:30 AM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/word-break-ii/

Given a string **A** and a dictionary of words **B**, add spaces in **A** to construct a sentence where each word is a valid dictionary word.

Return all such possible sentences.

**Note :** Make sure the strings are sorted in your result.

**Input Format:**

```
The first argument is a string, A.
The second argument is an array of strings, B.

```

**Output Format:**

```
Return a vector of strings representing the answer as described in the problem statement.

```

**Constraints:**

```
1 <= len(A) <= 50
1 <= len(B) <= 25
1 <= len(B[i]) <= 20

```

**Examples:**

```
Input 1:
    A = "b"
    B = ["aabbb"]

Output 1:
    []

Input 1:
    A = "catsanddog",
    B = ["cat", "cats", "and", "sand", "dog"]

Output 1:
    ["cat sand dog", "cats and dog"]

```

```cpp
vector<string> rec(const string& sentence, const vector<string>& dict,
    unordered_map<string, vector<string>>& found) {
    
    if(found.count(sentence)) {
        return found[sentence];
    }

    int n = sentence.size();
    vector<string> result;
    for(int i = 1; i <= n; i++) {
        string word = sentence.substr(0, i);
        string rem = sentence.substr(i);
        if(find(dict.begin(), dict.end(), word) != dict.end()) {
            if(rem.empty()) {
                result.push_back(word);
            }
            else {
                for(auto& s: rec(rem, dict, found)) {
                    result.push_back(word + " " + s);
                }
            }
        }
    }

    found[sentence] = result;
    return result;
}

vector<string> Solution::wordBreak(string A, vector<string> &B) {
    
    unordered_map<string, vector<string>> found;
    return rec(A, B, found);
}
```