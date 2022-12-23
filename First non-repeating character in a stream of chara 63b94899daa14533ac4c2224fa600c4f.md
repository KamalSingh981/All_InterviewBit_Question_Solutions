# First non-repeating character in a stream of characters | Interviewbit

Created: June 20, 2022 4:51 PM
Tags: Queue
URL: https://www.interviewbit.com/problems/first-non-repeating-character-in-a-stream-of-characters/

**Problem Description**

Given a string **A** denoting a stream of lowercase alphabets. You have to make new string **B**.

**B** is formed such that we have to find first non-repeating character each time a character is inserted to the stream and append it at the end to **B**. If no non-repeating character is found then append **'#'** at the end of **B**.

**Problem Constraints**

**Input Format**

The only argument given is string A.

**Output Format**

Return a string B after processing the stream of lowercase alphabets A.

**Example Input**

Input 1:

```
 A = "abadbc"
```

Input 2:

```
 A = "abcabc"
```

**Example Output**

Output 1:

```
 "aabbdd"
```

Output 2:

```
 "aaabc#"
```

**Example Explanation**

Explanation 1:

```
    "a"      -   first non repeating character 'a'
    "ab"     -   first non repeating character 'a'
    "aba"    -   first non repeating character 'b'
    "abad"   -   first non repeating character 'b'
    "abadb"  -   first non repeating character 'd'
    "abadbc" -   first non repeating character 'd'
```

Explanation 2:

```
    "a"      -   first non repeating character 'a'
    "ab"     -   first non repeating character 'a'
    "abc"    -   first non repeating character 'a'
    "abca"   -   first non repeating character 'b'
    "abcab"  -   first non repeating character 'c'
    "abcabc" -   no non repeating character so '#'
```

```cpp
string Solution::solve(string A) {
    queue<char> q;
    vector<int> v(26);
    string ans = "";
    for(int i = 0; i<A.length(); i++){
        v[A[i]-'a']++;
        q.push(A[i]);
        while(!q.empty()){
            if(v[q.front()-'a']>1){
                    q.pop();
                }
            else{
                ans += q.front();
                break;
            }
        }
        if(q.empty()){
            ans += '#';
        }
    }
    return ans;
}
```