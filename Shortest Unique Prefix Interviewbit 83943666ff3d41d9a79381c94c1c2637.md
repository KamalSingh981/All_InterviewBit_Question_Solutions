# Shortest Unique Prefix | Interviewbit

Created: July 23, 2022 11:34 PM
Tags: Trie
URL: https://www.interviewbit.com/problems/shortest-unique-prefix/

Find shortest unique prefix to represent each word in the list.

**Example:**

```
Input: [zebra, dog, duck, dove]
Output: {z, dog, du, dov}
where we can see that
zebra = z
dog = dog
duck = du
dove = dov

```

> 
> 
> 
> *NOTE* : Assume that no word is prefix of another. In other words, the representation is always possible.
> 

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
struct Trie{
    Trie *edge[26];
    int words;
    Trie(){
        for(auto i = 0; i<26; ++i){
            edge[i] = NULL;
        }
        words = 0;
    }
};

void addToTrie(Trie* head, string s){
    int n = s.length();
    Trie *current = head;
    
    for(auto i =0; i<n; ++i){
        current->words += 1;
        if(!current->edge[s[i] - 'a']){
            current->edge[s[i] - 'a'] = new Trie();
        }
        current = current->edge[s[i] - 'a'];
    }
}

string findPrefix(Trie * head, string s){
    int n = s.length();
    string prefix = "";
    Trie *current = head;
    int i = 0;
    current = current->edge[s[i] - 'a'];
    prefix += s[i];
    
    for(i = 1; i<n; ++i){
        if(current -> words == 1){
            return prefix;
        }
            current = current->edge[s[i]-'a'];
            prefix += s[i];    
    }
    return prefix;
}

vector<string> Solution::prefix(vector<string> &A) {
    vector<string> res;
    if(A.empty())
        return res;
    Trie *head = new Trie();
    
    auto size = A.size();
    
    for(auto i = 0; i<size; ++i){
        addToTrie(head, A[i]);
    }
    for(auto j = 0; j<size; ++j){
        res.emplace_back(findPrefix(head, A[j]));
        
    }
    
    return res;
}
```