# Convert the amount in number to words | Interviewbit

Created: June 15, 2022 1:41 PM
Tags: String
URL: https://www.interviewbit.com/problems/convert-the-amount-in-number-to-words/

Our company wants to create a data entry verification system. 
 Given an amount in words and an amount indicated by data entry person in numbers, you have to detect whether the amounts are same or not.

**Note**: There are a lot of corner cases to be considered. Interviewer expects you to take care of them.

**Input:**

```
String num: Amount written in digits as a string. This string will be an integer number without having any commas in between the digits.
String words: Amount written in words according to Indian Numbering System.

```

**Output:**

```
An integer
1: Values match
0: Otherwise

```

**Please note** :`Every word needs to be separated using "-" rather than a space character
 https://en.wikipedia.org/wiki/Indian_numbering_system`

**Constraints** 
 The number will fall in integer range(10^9)

**Example :**

```
Input :
String  num = "1234"
String words  = "one-thousand-two-hundred-and-thirty-four"

Output:
1

```

“Use Expected Output option” to clear the further doubts.

```cpp
string one[] = {"", "one-", "two-", "three-", "four-", "five-", "six-", "seven-", "eight-", "nine-", "ten-", "eleven-", "twelve-", "thirteen-", "fourteen-", "fifteen-", "sixteen-", "seventeen-", "eighteen-", "nineteen-"};

// strings at index 0 and 1 are not used, they is to

// make array indexing simple

string ten[] = {"", "", "twenty-", "thirty-", "forty-", "fifty-", "sixty-", "seventy-", "eighty-", "ninety-"};

// n is 1- or 2-digit number

string numToWords(int n, string s)

{

    string str = "";

    // if n is more than 19, divide it

    if (n > 19)

        str += ten[n / 10] + one[n % 10];

    else

        str += one[n];

    // if n is non-zero

    if (n)

        str += s;

    return str;

}

// Function to print a given number in words

string convertToWords(long n)

{

    // stores word representation of given number n

    string out;

    // handles digits at ten millions and hundred

    // millions places (if any)

    out += numToWords((n / 10000000), "crore-");

    // handles digits at hundred thousands and one

    // millions places (if any)

    out += numToWords(((n / 100000) % 100), "lakh-");

    // handles digits at thousands and tens thousands

    // places (if any)

    out += numToWords(((n / 1000) % 100), "thousand-");

    // handles digit at hundreds places (if any)

    out += numToWords(((n / 100) % 10), "hundred-");

    if (n > 100 && n % 100)

        out += "and-";

    // handles digits at ones and tens places (if any)

    out += numToWords((n % 100), "");

    // Handling the n=0 case

    if (out == "")

        out = "zero";

    return out;

}

int Solution::solve(string A, string B) {

    string s = convertToWords(stoi(A));

    while(s.back() == '-' || s.back() == ' ')

        s.erase(s.end()-1);

    // cout << s << endl;

    if(s == B)

        return 1;

    return 0;
}
```