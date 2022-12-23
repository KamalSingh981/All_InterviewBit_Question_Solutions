# String And Its Frequency | Interviewbit

Created: May 9, 2022 2:02 AM
URL: https://www.interviewbit.com/problems/string-and-its-frequency/

**Problem Description**

Given a string **A** with lowercase english alphabets and you have to return a string in which, with each character its frequency is written in adjacent.

**Problem Constraints**

**Input Format**

**Output Format**

**Example Input**

Input 1:

```
abbhuabcfghh

```

Input 2:

```
a

```

**Example Output**

Ouput 1:

```
a2b3h3u1c1f1g1

```

Ouput 2:

```
a1

```

**Example Explanation**

Explanation 1:

```
‘a’ occurs in the string a total of 2 times so we write a2 then ‘b’ occurs a total of 3 times so next we write b3 and so on
```

Explanation 2:

```
‘a’ occurs in the string a total of 1 time only.

```

```cpp
string Solution::solve(string A) {
    vector<string> a(26,"");
    vector<int> b(26,0);
    vector<int> order(26,-1);
    int count = 0;
    for(int i =0; i<A.length(); i++){
        b[A[i]-97] += 1;
        if(b[A[i]-97] == 1){
            a[A[i]-97] = A[i];
            order[count] = A[i] -97;
            count++;
        }
    }
    string ans;
    for(int i=0; i<26; i++){
        if(order[i]!=-1){
            ans += (a[order[i]]) + to_string(b[order[i]]);
        }
    }
    return ans;
}
```