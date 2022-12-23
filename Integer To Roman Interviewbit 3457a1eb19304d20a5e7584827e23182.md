# Integer To Roman | Interviewbit

Created: June 15, 2022 12:50 AM
Tags: String
URL: https://www.interviewbit.com/problems/integer-to-roman/

Another question which belongs to the category of questions which are intentionally stated vaguely. 
 Expectation is that you will ask for correct clarification or you will state your assumptions before you start coding.

Given an integer **A**, convert it to a roman numeral, and return a string corresponding to its roman numeral version

> 
> 
> 
> **Note :** This question has a lot of scope of clarification from the interviewer. Please take a moment to think of all the needed clarifications and see the expected response using “See Expected Output”
> 
> For the purpose of this question, **https://projecteuler.net/about=roman_numerals** has very detailed explanations.
> 

**Input Format**

```
The only argument given is integer A.

```

**Output Format**

```
Return a string denoting roman numeral version of A.

```

**Constraints**

```
1 <= A <= 3999

```

**For Example**

```
Input 1:
    A = 5
Output 1:
    "V"

Input 2:
    A = 14
Output 2:
    "XIV"

```

```cpp
string Solution::intToRoman(int A) {
    vector<pair<string, int>> roman = {{"I", 1},{"IV", 4},{"V", 5}, {"IX", 9},{"X", 10},{"XL", 40},
                        {"L", 50},{"XC", 90},{"C", 100}, {"CD", 400},{"D", 500},{"CM", 900}, {"M", 1000}};
    string ans = "";
    for(int i = roman.size()-1; i>=0; i--){
        if(A/(roman[i].second)){
            int q= 0;
            while(q<A/(roman[i].second)){
                ans  += roman[i].first;
                q++; 
            }
            A = A%(roman[i].second);
        }
    }
    return ans;
}
```