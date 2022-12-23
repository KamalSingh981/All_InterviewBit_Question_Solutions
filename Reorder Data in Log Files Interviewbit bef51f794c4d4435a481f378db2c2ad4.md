# Reorder Data in Log Files | Interviewbit

Created: May 12, 2022 11:43 PM
URL: https://www.interviewbit.com/problems/reorder-data-in-log-files/

**Problem Description**

You are given an array of logs. Each log is a space-delimited string of words, where the first word is the identifier.

There are two types of logs:

- Letter-logs: All words (except the identifier) consist of lowercase English letters.
- Digit-logs: All words (except the identifier) consist of digits.

Reorder these logs so that:

- The letter-logs come before all digit-logs.
- The letter-logs are sorted lexicographically by their contents. If their contents are the same, then sort them lexicographically by their identifiers.
- The digit-logs maintain their relative ordering.

Return the final order of the logs.

**Problem Constraints**

1 <= logs.length <= 1000
 3 <= logs[i].length <= 1000
 All the tokens of logs[i] are separated by a single space.
 logs[i] is guaranteed to have an identifier and at least one word after the identifier.

**Input Format**

**Output Format**

**Example Input**

Input 1:

```
A = ["dig1-8-1-5-1", "let1-art-can", "dig2-3-6", "let2-own-kit-dig", "let3-art-zero"]

```

Input 2:

```
A = ["a1-9-2-3-1","g1-act-car","zo4-4-7","ab1-off-key-dog","a8-act-zoo"]

```

**Example Output**

Output 1:

```
["let1-art-can","let3-art-zero","let2-own-kit-dig","dig1-8-1-5-1","dig2-3-6"]

```

Output 2:

```
["g1-act-car", "a8-act-zoo", "ab1-off-key-dog", "a1-9-2-3-1", "zo4-4-7"]

```

**Example Explanation**

Explanation 1:

```
The letter-log contents are all different, so their ordering is "art-can", "art-zero", "own-kit-dig".
The digit-logs have a relative order of "dig1-8-1-5-1", "dig2-3-6".

```

Explanation 2:

```
The array has been sorted restricted to the conditions given.

```

```python
class Solution:
    # @param A : list of strings
    # @return a list of strings
    def reorderLogs(self, A):
        ans = []
        alph = []
        for i in A:
            for j in range(len(i)):
                if i[j] == "-" and i[j+1].isdigit():
                    ans.append(i)
                    break
                elif i[j] == "-" and i[j+1].isalpha():
                    alph.append(i.split("-"))
                    break
        alph.sort(key = lambda x :x[0])
        alph.sort(key = lambda x : x[1:])
        for i in range(len(alph)):
            alph[i] = ("-".join(alph[i]))
        return alph+ans
```

```cpp
bool cmp(pair<string,string>&a,pair<string,string>&b){
    return a.first < b.first;
}

vector<string> Solution::reorderLogs(vector<string> &A) {
    int n = A.size();
    vector<pair<string,string>> letlog;
    vector<string>diglog;
    for(auto x:A){
        int j=0;
        while(x[j] !='-'){
            j++;
        }
        if(x[j+1] >= '0' && x[j+1]<='9'){
            diglog.push_back(x);
        } else {
            pair<string,string>temp;
            temp.first = x.substr(j);
            temp.second = x.substr(0,j);
            letlog.push_back(temp);
        }
    }
    sort(letlog.begin(),letlog.end(),cmp);

    vector<string>ans;
    for(auto x:letlog){
        string temp = x.second + x.first;
        ans.push_back(temp);
    }
    for(auto x:diglog){
        ans.push_back(x);
    }

    return ans;
}
```