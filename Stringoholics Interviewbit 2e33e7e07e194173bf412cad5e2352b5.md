# Stringoholics | Interviewbit

Created: June 14, 2022 5:26 PM
Tags: String
URL: https://www.interviewbit.com/problems/stringoholics/

**Problem Description**

You are given an array **A** consisting of strings made up of the letters 'a' and 'b' only.
Each string goes through a number of operations, where:

```
1.  At time 1, you circularly rotate each string by 1 letter.
2.  At time 2, you circularly rotate the new rotated strings by 2 letters.
3.  At time 3, you circularly rotate the new rotated strings by 3 letters.
4.  At time i, you circularly rotate the new rotated strings by i % length(string) letters.

Eg: String is "abaa" At time 1, string is "baaa", as 1 letter is circularly rotated to the back At time 2, string is "aaba", as 2 letters of the string "baaa" is circularly rotated to the back At time 3, string is "aaab", as 3 letters of the string "aaba" is circularly rotated to the back At time 4, string is again "aaab", as 4 letters of the string "aaab" is circularly rotated to the back At time 5, string is "aaba", as 1 letters of the string "aaab" is circularly rotated to the back

```

After some units of time, a string becomes equal to its original self.
Once a string becomes equal to itself, it's letters start to rotate from the first letter again (**process resets**). So, if a string takes **t** time to get back to the original, at time t+1 one letter will be rotated and the string will be its original self at 2**t** time.
You have to find the minimum time, where maximum number of strings are equal to their original self.
As this time can be very large, give the answer modulo **109+7**.

**Note:** Your solution will run on multiple test cases so do clear global variables after using them.

**Input Format**

**Output Format**

Minimum time, where maximum number of strings are equal to their original self.

**Example Input**

Input 1:

```
  A: [a, ababa, aba]

```

Input 2:

```
  A : [a, aa]

```

**Example Output**

Output 1:

```
  4

```

Output 2:

```
  1

```

**Example Explanation**

Explanation 1:

```
  String 'a' is it's original self at time 1, 2, 3 and 4.
String 'ababa' is it's original self only at time 4. (ababa => babaa => baaba => babaa => ababa)
String 'aba' is it's original self at time 2 and 4. (aba => baa => aba)
Hence, 3 strings are their original self at time 4.

```

Explanation 2:

```
  Both strings are their original self at time 1.

```

```cpp
#define mod 1000000007
#define ll long long
ll smallestString(string &pat) { // KMP - LPS
    // length of the previous longest prefix suffix 
    ll M = pat.size();
    int len = 0; 
    int lps[M];
    lps[0] = 0; // lps[0] is always 0 
  
    // the loop calculates lps[i] for i = 1 to M-1 
    int i = 1; 
    while (i < M) { 
        if (pat[i] == pat[len]) { 
            len++; 
            lps[i] = len; 
            i++; 
        } 
        else // (pat[i] != pat[len]) 
        { 
            // This is tricky. Consider the example. 
            // AAACAAAA and i = 7. The idea is similar 
            // to search step. 
            if (len != 0) { 
                len = lps[len - 1]; 
  
                // Also, note that we do not increment 
                // i here 
            } 
            else // if (len == 0) 
            { 
                lps[i] = 0; 
                i++; 
            } 
        } 
    } 
    // Now we have to find the size of smallest substring that can be repeated to get the whole string.
    ll t1 = lps[M-1];
    ll t2 = M-t1;
    if(t1 < t2) return M;
    else if(t1 % t2 != 0) return M;
    else return t2;
} 

int Solution::solve(vector<string> &A) {
     int l = 1,len=A.size(),h;
    vector<ll> v(len);
    
    for(int i=0;i<len;i++){
        ll n = smallestString(A[i]); 
        ll k = 1;
        while(1){
          ll changes = (k*(k+1))/2; 
          if(changes%n==0){
              v[i]=k;
              break;
          }
            k++;
        }
    }
    
    ll ans=1;
    for(ll i=0;i<len;i++){
        for(ll j=i+1;j<len && v[i]!=1 ;j++){
            v[j] = v[j]/__gcd(v[j], v[i]);
        }
        ans = 1ll*(ans%mod*(v[i])%mod)%mod;
    }
    return ans%mod;
 return ans%mod;
    
}
```