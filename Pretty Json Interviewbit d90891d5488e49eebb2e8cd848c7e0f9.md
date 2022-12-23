# Pretty Json | Interviewbit

Created: June 17, 2022 7:01 PM
Tags: String
URL: https://www.interviewbit.com/problems/pretty-json/

Given a string **A** representating json object. Return an array of string denoting json object with proper indentaion.

Rules for proper indentaion:

- Every inner brace should increase one indentation to the following lines.
- Every close brace should decrease one indentation to the same line and the following lines.
- **The indents can be increased with an additional ‘\t’**

**Note**:

1. 
    
    `[]` and `{}` are only acceptable braces in this case.
    
2. 
    
    Assume for this problem that space characters can be done away with.
    

**Input Format**

```
The only argument given is the integer array A.

```

**Output Format**

```
Return a list of strings, where each entry corresponds to a single line. The strings should not have "\n" character in them.

```

**For Example**

```
Input 1:
    A = "{A:"B",C:{D:"E",F:{G:"H",I:"J"}}}"
Output 1:
    {
        A:"B",
        C:
        {
            D:"E",
            F:
            {
                G:"H",
                I:"J"
            }
        }
    }

Input 2:
    A = ["foo", {"bar":["baz",null,1.0,2]}]
Output 2:
   [
        "foo",
        {
            "bar":
            [
                "baz",
                null,
                1.0,
                2
            ]
        }
    ]

```

```cpp
vector<string> Solution::prettyJSON(string s) {
    vector<string> res;
    int n = s.size();
    int indent =0;
    char last  = '$';
    string temp = "";
    
    for(int i=0; i<n; i++){
        
        char ch = s[i];
        if(ch == ' '){
            continue;
        }
        if(ch == '}' || ch == ']'){
            indent--;
        }
        
        
        if(last == '{' || last == '[' || ch == '}' || ch ==']' || (last == ',') || (last==':' && (ch == '{' || ch=='['))){
            res.push_back(temp);
            temp = "";
            for(int j = 0; j<indent; j++){
                temp += "\t";
            }
        }
        
        if(ch == '{' || ch == '['){
            indent++;
        }
        temp += ch;
        last = ch;
     }
    if(temp != ""){
        res.push_back(temp);
    }
        
    return res;
}
```