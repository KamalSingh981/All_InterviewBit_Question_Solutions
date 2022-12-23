# Anagrams | Interviewbit

Created: July 16, 2022 1:00 AM
Tags: Hashing
URL: https://www.interviewbit.com/problems/anagrams/

Given an array of strings, return all groups of strings that are anagrams. Represent a group by a list of integers representing the index in the original list. Look at the sample case for clarification.

> 
> 
> 
> **Anagram :** a word, phrase, or name formed by rearranging the letters of another, such as `'spar'`, formed from `'rasp'`
> 

> 
> 
> 
> **Note:** All inputs will be in lower-case.
> 

**Example :**

```
Input : cat dog god tca
Output : [[1, 4], [2, 3]]

```

`cat` and `tca` are anagrams which correspond to index `1` and `4`. `dog` and `god` are another set of anagrams which correspond to index `2` and `3`.
 The indices are 1 based ( the first element has index 1 instead of index 0).

> 
> 
> 
> **Ordering of the result :** You should not change the relative ordering of the words / phrases within the group. Within a group containing `A[i]` and `A[j]`, `A[i]` comes before `A[j]` if `i < j`.
> 

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
vector<vector<int> > Solution::anagrams(const vector<string> &A) {
    vector<vector<int>> ans; // variable for storing the ans
    map<map<char, int>, vector<int>> index; // we are creating a map of map for storing the 
                                            //count of a word and its charctar and vector for storing 
                                            //the indexes of anagras 
    for(int i = 0; i<A.size(); i++){
        map<char, int> tm;
        for(int j = 0; j<A[i].size(); j++){
                tm[A[i][j]]++; // counting the occurrence of a character in a word
            }
        index[tm].push_back(i+1);
    }
    
    for(auto i: index){
        ans.push_back(i.second); // appending the ans list to the vector
    }
    return ans;
}
```