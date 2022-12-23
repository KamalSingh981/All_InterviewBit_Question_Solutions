# Scramble String | Interviewbit

Created: August 6, 2022 1:12 AM
Tags: Dynamic Programming
URL: https://www.interviewbit.com/problems/scramble-string/

Given a string **A**, we may represent it as a binary tree by partitioning it to two non-empty substrings recursively.

Below is one possible representation of **A = “great”**:

```

    great
   /    \
  gr    eat
 / \    /  \
g   r  e   at
           / \
          a   t

```

To scramble the string, we may choose any non-leaf node and swap its two children.

For example, if we choose the node “gr” and swap its two children, it produces a scrambled string “rgeat”.

```
    rgeat
   /    \
  rg    eat
 / \    /  \
r   g  e   at
           / \
          a   t

```

We say that “rgeat” is a scrambled string of “great”.

Similarly, if we continue to swap the children of nodes “eat” and “at”, it produces a scrambled string “rgtae”.

```
    rgtae
   /    \
  rg    tae
 / \    /  \
r   g  ta  e
       / \
      t   a

```

We say that “rgtae” is a scrambled string of “great”.

Given two strings **A** and **B** of the same length, determine if **B** is a scrambled string of **S**.

**Input Format:**

```
The first argument of input contains a string A.
The second argument of input contains a string B.

```

**Output Format:**

```
Return an integer, 0 or 1:
    => 0 : False
    => 1 : True

```

**Constraints:**

```
1 <= len(A), len(B) <= 50

```

**Examples:**

```
Input 1:
    A = "we"
    B = "we"

Output 1:
    1

Input 2:
    A = "phqtrnilf"
    B = "ilthnqrpf"

Output 2:
    0

```

```cpp
bool isPossible(string a, string b, int n, unordered_map<string, bool> &m){
    if(a == b) return m[a + "%" + b] = true;
    else if(n == 1) return false;
    else if(m.find(a + "%" + b) != m.end()) return m[a + "%" + b];
    
    for(int k = 1; k<n; k++){
        bool cond1 = isPossible(a.substr(0, k), b.substr(0, k), k ,m) and isPossible(a.substr(k, n-k), b.substr(k, n-k), n-k,m);
        bool cond2 = isPossible(a.substr(k, n-k), b.substr(0, n-k), n-k,m) and isPossible(a.substr(0, k), b.substr(n-k, k), k,m);
        if(cond1 || cond2){
            return m[a + "%" + b] = true;
        }
    }
    return m[a + "%" + b] = false;
}

int Solution::isScramble(const string A, const string B) {
    unordered_map<string, bool> m;
    
    int n = A.length();
    int q = B.length();
    if(n != q) return false;
    
    return isPossible(A, B, n, m);
}
```

[https://www.youtube.com/watch?v=H10na5jb4Ck](https://www.youtube.com/watch?v=H10na5jb4Ck)