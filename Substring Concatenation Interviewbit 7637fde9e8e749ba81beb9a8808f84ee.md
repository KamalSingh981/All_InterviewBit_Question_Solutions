# Substring Concatenation | Interviewbit

Created: July 15, 2022 11:37 PM
Tags: Hashing
URL: https://www.interviewbit.com/problems/substring-concatenation/

You are given a string, S, and a list of words, L, that are all of the same length.

Find all starting indices of `substring(s)` in `S` that is a concatenation of each word in `L` exactly once and without any intervening characters.

**Example :**

```
S: "barfoothefoobarman"
L: ["foo", "bar"]

```

You should return the indices: `[0,9]`.
 (order does not matter).

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
vector<int> Solution::findSubstring(string A, const vector<string> &B) {
    map<string, int> words; // Storing the words in the map with there count
    for(int i = 0; i<B.size();i++){
        words[B[i]]++;
    }
    int lenstr = B[0].length(); // length of the word findSubstring
    int arrsize = B.size(); // size of the array
    
    vector<int> ans; // stores the ans
    int t = A.length()-lenstr +1;
    for(int i = 0; i<t; i++){ // iteration from every character
        if(words[A.substr(i, lenstr)]>0){
            map<string, int> d; // this map is for storing the words and count which are found the the string
            d[A.substr(i, lenstr)]++;
            int c = 1;
            int j  = i + lenstr; // iterating through the string
            while(c<arrsize and j<t){
                string temp = A.substr(j, lenstr);
                d[temp]++;
                if(words[temp] <= 0 or d[temp] > words[temp]){ // if the next word is not present in the 
                                                                //words list or if the word is count becomes 
                                                                //more than the count in the words list then 
                                                                //break it.
                
                    break;
                }
                j += lenstr;
                c += 1;
            }
            if(c == arrsize){ // if the while complete without breaking the add the index to the ans
                ans.push_back(i);
            }
        }
    }   
    return ans; // return the ans;
}
```