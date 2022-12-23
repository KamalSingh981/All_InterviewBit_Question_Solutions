# Roman To Integer | Interviewbit

Created: June 15, 2022 1:18 AM
Tags: String
URL: https://www.interviewbit.com/problems/roman-to-integer/

Given a string **A** representing a roman numeral.
 Convert **A** into integer.

**A** is guaranteed to be within the range from **1** to **3999**.

**NOTE**: Read more 
 details about roman numerals at [Roman Numeric System](https://en.wikipedia.org/wiki/Roman_numerals#Roman_numeric_system)

**Input Format**

```
The only argument given is string A.

```

**Output Format**

```
Return an integer which is the integer verison of roman numeral string.

```

**For Example**

```
Input 1:
    A = "XIV"
Output 1:
    14

Input 2:
    A = "XX"
Output 2:
    20

```

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

### My first code

```cpp
int Solution::romanToInt(string A) { 
        int ans = 0;
        for(int i = 0; i<A.length(); i++){
            if(A.substr(i,2) == "XL"){
                ans += 40;
                i++;
            }
            else if(A.substr(i,2) == "IV"){
                ans += 4;
                i++;
            }
            else if(A.substr(i,2) == "IX"){
                ans += 9;
                i++;
            }
            else if(A.substr(i,2) == "XC"){
                ans += 90;
                i++;
            }
            
            else if(A.substr(i,2) == "CD"){
                ans += 400;
                i++;
            }
            else if(A.substr(i,2) == "CM"){
                ans += 900;
                i++;
            }
            else if(A[i] == 'I'){
                ans += 1;
            }
            else if(A[i] == 'V'){
                ans += 5;
            }
            else if(A[i] == 'X'){
                ans += 10;
            }
            else if(A[i] == 'L'){
                ans += 50;
            }
            else if(A[i] == 'C'){
                ans += 100;
            }
            else if(A[i] == 'D'){
                ans += 500;
            }
            else if(A[i] == 'M'){
                ans += 1000;
            }   
        }
        
    return ans;
}
```

Other Code

```cpp
int Solution::romanToInt(string A) { 
        map<char, int> m;
        m.insert({ 'I', 1 });
        m.insert({ 'V', 5 });
        m.insert({ 'X', 10 });
        m.insert({ 'L', 50 });
        m.insert({ 'C', 100 });
        m.insert({ 'D', 500 });
        m.insert({ 'M', 1000 });
        int ans=  0;
        for(int i = 0; i<A.length(); i++){
            if(i<A.length() - 1 && m[A[i]]<m[A[i+1]]){
                ans -= m[A[i]];
            }
            else{
                ans += m[A[i]];
            }
        } 
    return ans;
}
```