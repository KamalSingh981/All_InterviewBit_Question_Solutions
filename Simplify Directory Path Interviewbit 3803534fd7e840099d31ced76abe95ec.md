# Simplify Directory Path | Interviewbit

Created: June 19, 2022 3:28 PM
Tags: Stacks
URL: https://www.interviewbit.com/problems/simplify-directory-path/

Given a string **A** representing an absolute path for a file (Unix-style).

Return the string A after simplifying the absolute path.

**Note**:

In Unix-style file system:

- A period '.' refers to the current directory.
- A double period '..' refers to the directory up a level.
- Any multiple consecutive slashes '//' are treated as a single slash '/'.

In Simplified Absolute path:

- The path starts with a single slash '/'.
- Any two directories are separated by a single slash '/'.
- The path doesn't end with trailing slashes '/'.
- The path only contains the directories on the path from the root directory to the target file or directory (i.e., no period '.' or double period '..')
- Path will not have whitespace characters.

**Input Format**

```
The only argument given is string A.

```

**Output Format**

```
Return a string denoting the simplified absolue path for a file (Unix-style).

```

**For Example**

```cpp
vector<string> splitStrings(string str, char dl)
{
    string word = "";
 
    // to count the number of split strings
    int num = 0;
 
    // adding delimiter character at the end
    // of 'str'
    str = str + dl;
 
    // length of 'str'
    int l = str.size();
 
    // traversing 'str' from left to right
    vector<string> substr_list;
    for (int i = 0; i < l; i++) {
 
        // if str[i] is not equal to the delimiter
        // character then accumulate it to 'word'
        if (str[i] != dl)
            word = word + str[i];
 
        else {
 
            // if 'word' is not an empty string,
            // then add this 'word' to the array
            // 'substr_list[]'
            if ((int)word.size() != 0)
                substr_list.push_back(word);
 
            // reset 'word'
            word = "";
        }
    }
 
    // return the splitted strings
    return substr_list;
}
string Solution::simplifyPath(string A) {
    vector<string> a;
    string ans = "";
    vector<string> word= splitStrings(A, '/');
    for(int i=0; i<word.size(); i++){
        if(word[i] == "" || word[i] == ".") continue;
        else if(a.size() !=0 && word[i] == ".."){a.pop_back();}
        else if(word[i] != ".."){
            a.push_back(word[i]);
        }
    }
    
    if(a.size() == 0){
        return "/";
    }
    for(int i=0; i<a.size(); i++){
        ans += "/" + a[i];
    }
    return ans;
    
}
```

Using the Stack data structure, But this implementation is bit slow

```cpp
string Solution::simplifyPath(string A) {
    stack<string> a;
    string ans = "";
    for(int i=0; i<A.length(); i++){
        string s = "";
        while(i<A.length() && A[i] != '/'){
            s += A[i++]; 
        }
        if(s == "" || s == ".") continue;
        else if(!a.empty() && s == ".."){a.pop();}
        else if(s != ".."){
            a.push(s);
        }
    }
    
    if(a.empty()){
        return "/";
    }
    while(!a.empty()){
        ans.insert(0, a.top());
        ans.insert(0,"/");
        a.pop();
    }
    return ans;
    
}
```