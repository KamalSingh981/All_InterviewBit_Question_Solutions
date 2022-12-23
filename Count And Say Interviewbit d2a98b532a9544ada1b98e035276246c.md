# Count And Say | Interviewbit

Created: June 14, 2022 1:34 PM
Tags: String
URL: https://www.interviewbit.com/problems/count-and-say/

**Problem Description**

The count-and-say sequence is the sequence of integers beginning as follows:  1 is read off as one 1 or 11. 11 is read off as two 1s or 21.

21 is read off as one 2, then one 1 or 1211.

Given an integer n, generate the nth sequence.

Note: The sequence of integers will be represented as a string.

**Example:**

if n = 2, the sequence is 11.

```cpp
string Solution::countAndSay(int A) {
    if(A==1){
       return "1";
   }
   else if(A == 2){
       return "11";
   }
    int count = 1;
    string s = "21";
    string t = "";
    for(int i=0; i<A-3; i++){
        for(int j = 0; j<s.length(); j++){
            if(s[j] == s[j + 1] && s.length()-1>j){
                count++;
            }
            else{
                t += to_string(count);
                t += s[j];
                count = 1;
            }
        }
        s = t;
        t = "";
    }
    return s;  
}
```