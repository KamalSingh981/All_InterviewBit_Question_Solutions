# Colorful Number | Interviewbit

Created: July 14, 2022 11:29 PM
Tags: Hashing
URL: https://www.interviewbit.com/problems/colorful-number/

For Given Number `N` find if its **COLORFUL** number or not

**Return 0/1**

**COLORFUL number:**

```
A number can be broken into different contiguous sub-subsequence parts.
Suppose, a number 3245 can be broken into parts like 3 2 4 5 32 24 45 324 245.
And this number is a COLORFUL number, since product of every digit of a contiguous subsequence is different

```

**Example:**

```
N = 23
2 3 23
2 -> 2
3 -> 3
23 -> 6
this number is a COLORFUL number since product of every digit of a sub-sequence are different.

Output : 1

```

```cpp
int Solution::colorful(int A) {
    
    
    unordered_map<int, int> m;
    string a = to_string(A);
    int  d = 1;
    for(int d = 1; d<=a.length(); d++){
        for(int i = 0; (i+d)<=a.length(); i++){
            string temp = a.substr(i, d);
            int value = 1;
            for(int j = 0; j<temp.length(); j++){
                value = value*(temp[j] - '0');
            }
            m[value]++;
        }
    }
    for(auto s:m){
        if(s.second > 1){
            return 0;
        }   
    }
    return 1;
}
```