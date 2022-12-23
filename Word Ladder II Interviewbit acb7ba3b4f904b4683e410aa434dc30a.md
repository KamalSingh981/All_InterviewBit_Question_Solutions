# Word Ladder II | Interviewbit

Created: July 29, 2022 10:49 PM
Tags: Graphs
URL: https://www.interviewbit.com/problems/word-ladder-ii/

```cpp
// this function is used to get all the words which differ by atmost one character with the previous word
    vector<string> get(string word,unordered_set<string> wordList){
        vector<string> ans;
        for(int i=0;i<word.length();i++){
            char ch = word[i];
            for(char c = 'a';c<='z';c++){
                word[i] = c; // change the ith character and check
                if(wordList.count(word)) // push those words in ans which differ by atmost one character
                    // and present in wordList
                    ans.push_back(word);
            }
            word[i] = ch;
        }
        return ans;
    }

vector<vector<string> > Solution::findLadders(string beginWord, string endWord, vector<string>& wordList) {
    bool found = false;
    if(beginWord == endWord){
        return {{beginWord}};
    } // check whether we have found the answer ?
        queue<vector<string>> q; // queue of paths
        vector<vector<string>> ans; // all shortest transformations
        unordered_set<string> visited; // store which words are already visited
        unordered_set<string> all_words(wordList.begin(),wordList.end()); // store all words in wordList in unordered set
        q.push({beginWord});
        while(!q.empty()){
            // process all paths upto current level
            int paths = q.size();
            for(int i=0;i<paths;i++){
                vector<string> curr = q.front();
                q.pop();
                // find all those words which can be inserted at the back of current path
                vector<string> words = get(curr.back(),all_words);
                for(auto s:words){
                    vector<string> new_path(curr.begin(),curr.end());
                    new_path.push_back(s);
                    if(s==endWord){
                        found = true;
                        ans.push_back(new_path);
                    }
                    visited.insert(s);
                    q.push(new_path);
                }
            }
            if(found)
                break;
            for(auto s:visited)
                all_words.erase(s);
            visited.clear();
        }
return ans;
}
```

Given two words (**start** and **end**), and a dictionary, find the shortest transformation sequence from **start** to **end**, such that:

> 
> 
> - Only one letter can be changed at a time
> - Each intermediate word must exist in the dictionary

If there are multiple such sequence of shortest length, return all of them. Refer to the example for more details.

**Note:**

> 
> 
> - All words have the same length.
> - All words contain only lowercase alphabetic characters.

**Input Format**

```
The first argument is string start.
The second argument is string end.
The third argument is an array of strings dict

```

**Output Format**

```
Return all transformation sequences such that first word of each sequence is start and last word is end, all intermediate words belongs to dictionary(dict) and consecutive words had atmost 1 difference.

```

**Example :**

:

```
start = "hit"
end = "cog"
dict = ["hot","dot","dog","lot","log"]

```

Return

```
  [
    ["hit","hot","dot","dog","cog"],
    ["hit","hot","lot","log","cog"]
  ]

```

![Word%20Ladder%20II%20Interviewbit%20acb7ba3b4f904b4683e410aa434dc30a/superman.e804d3.png](Word%20Ladder%20II%20Interviewbit%20acb7ba3b4f904b4683e410aa434dc30a/superman.e804d3.png)