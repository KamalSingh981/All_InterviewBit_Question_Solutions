# Convert to Palindrome | Interviewbit

Created: June 14, 2022 10:56 PM
Tags: String
URL: https://www.interviewbit.com/problems/convert-to-palindrome/

**Problem Description**

Given a string **A** consisting only of lowercase characters, we need to check whether it is possible to make this string a **palindrome** after removing exactly one character from this.

If it is possible then return **1** else return **0**.

**Problem Constraints**

3 <= |A| <= 105

A[i] is always a lowercase character.

**Input Format**

First and only argument is an string **A**.

**Output Format**

Return 1 if it is possible to convert **A** to palindrome by removing exactly one character else return 0.

**Example Input**

Input 1:

```
 A = "abcba"

```

Input 2:

```
 A = "abecbea"

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 We can remove character ‘c’ to make string palindrome

```

Explanation 2:

```
 It is not possible to make this string palindrome just by removing one character

```

Interviewbit Code

```cpp
int is(string A , int i , int j ){
    //if(j - i < 2) return 1 ; 
    while(i < j){
        if(A[i] == A[j]){
            i++ ; 
            j-- ; 
            
        }
        else{
            return 0 ;
        }
    }
    return 1 ;
}
int Solution::solve(string A) {
    int n = A.length() , i = 0 ;
    int j = n-1 , tag = -1 ; 
    for(; i < n ;){
        if(A[i] != A[j]){
            tag = (is(A , i+1 , j) || is(A , i , j-1)) ;
            return tag ;
        }
        i++ ; j-- ; 
    }
    return 1 ;
}
```

Mycode

```cpp
bool palindorme(string a){
    int n = a.length()-1;
    int i = 0;
    while(i<n){
        if(a[i] != a[n]){
            return false;
        }
        i++;
        n--;
    }
    return true;
}
int Solution::solve(string A) {
    int start = 0;
    int end = A.length() - 1;
    while(start<end){
        if(A[start] != A[end]){
            break;
        }
        start++;
        end--;
    }
    string s = A;
    bool ans1 = palindorme(s.erase(start, 1));
    bool ans2 = palindorme(A.erase(end, 1));
    if(ans1 || ans2){
        return 1;
    }
    else{
        return 0;
    }  
}
```