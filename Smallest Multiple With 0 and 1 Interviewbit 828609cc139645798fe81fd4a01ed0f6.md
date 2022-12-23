# Smallest Multiple With 0 and 1 | Interviewbit

Created: July 26, 2022 11:03 PM
Tags: BFS, Graphs
URL: https://www.interviewbit.com/problems/smallest-multiple-with-0-and-1/

You are given an integer N. You have to find smallest multiple of N which consists of digits `0` and `1` only. Since this multiple could be large, return it in form of a string.

**Note**:

- Returned string should not contain leading zeroes.

For example,

```cpp
string Solution::multiple(int A) {
    
    string t = "1";
    set<int> visit;
    queue<string> q;
    q.push(t);
    while(!q.empty()){
        t = q.front();
        q.pop();
        int rem = 0;
        for(int i = 0; i<t.length(); i++){
            rem = rem*10 + (t[i]- '0');
            rem = rem%A;
        }
        if(rem == 0){
            return t;
        }
        if(visit.find(rem) == visit.end()){
            visit.insert(rem);
            q.push(t + "0");
            q.push(t + "1");
        }
    } 
}
```