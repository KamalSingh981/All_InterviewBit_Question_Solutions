# Bulls and Cows | Interviewbit

Created: May 12, 2022 4:50 PM
URL: https://www.interviewbit.com/problems/bulls-and-cows/

**Problem Description**

You are playing the Bulls and Cows game with your friend.

You write down a secret number and ask your friend to guess what the number is. When your friend makes a guess, you provide a hint with the following info:

```
The number of "bulls", which are digits in the guess that are in the correct position.
The number of "cows", which are digits in the guess that are in your secret number but are located in the wrong position.
Specifically, the non-bull digits in the guess that could be rearranged such that they become bulls.
```

Given the secret number secret and your friend's guess guess, return the hint for your friend's guess.

The hint should be formatted as "xAyB", where x is the number of bulls and y is the number of cows. Note that both secret and guess may contain duplicate digits.

**Problem Constraints**

```
1 <= secret.length, guess.length <= 100000
secret.length == guess.length
secret and guess consist of digits only.

```

**Input Format**

First argument is string denoting secret string

Second argument is string denoting guess string

**Output Format**

**Example Input**

Input 1:

```
secret = "1807", guess = "7810"

```

Input 2:

```
secret = "1123", guess = "0111"

```

**Example Output**

**Example Explanation**

Explanation 1:

```
Bulls are connected with a '|':
"1807"
  |
"7810"
```

Explanation 2:

```
Bulls are connected with a '|'
"1123"        "1123"
  |      or     |
"0111"        "0111"
Note that only one of the two unmatched 1s is counted as a cow since
the non-bull digits can only be rearranged to allow one 1 to be a bull.
```

```python
string Solution::solve(string secret, string guess) {
        int len = secret.size();
        
        int secret_freq[10] = {0};
        int guess_freq[10] = {0};
        
        
        //Calculate freq of secret
        for(int idx = 0; idx < len; idx++) {
            int digit = secret[idx] - '0';
            secret_freq[digit]++;
        }
        
        //Calculate freq of guess
        for(int idx = 0; idx < len; idx++) {
            int digit = guess[idx] - '0';
            guess_freq[digit]++;
        }
        
        //Check for bulls (correct pos of elements)
        int bulls = 0;
        for(int idx = 0; idx < len; idx++ ) {
            if(secret[idx] == guess[idx]) {
                bulls++;
                int digit = secret[idx] - '0';
                secret_freq[digit]--;
                guess_freq[digit]--;
            }
        }
        
        int cows = 0;
        for(int idx = 0; idx < 10; idx++) {
            if(secret_freq[idx] > 0 && guess_freq[idx] > 0) {
                cows += min(secret_freq[idx], guess_freq[idx]);
            }
        }
        
        string bulls_str = to_string(bulls);
        string cows_str = to_string(cows);
        
        string res = bulls_str + "A" + cows_str + "B";

        
        return res;
}
```