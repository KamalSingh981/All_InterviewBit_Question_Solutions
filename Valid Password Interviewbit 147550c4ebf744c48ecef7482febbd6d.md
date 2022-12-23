# Valid Password | Interviewbit

Created: May 9, 2022 2:01 AM
URL: https://www.interviewbit.com/problems/valid-password/

**Problem Description**

Given a password as a character array **A**.
Check if it is valid or not.

- Password should have at least one numerical digit(0-9).
- Password's length should be in between 8 to 15 characters.
- Password should have at least one lowercase letter(a-z).
- Password should have at least one uppercase letter(A-Z).
- Password should have at least one special character ( @, #, %, &, !, $, *).

**Problem Constraints**

**Input Format**

**Output Format**

**Example Input**

Input 1:

```
A = ['S', 'c', 'a', 'l', 'e', 'r', '@', '1']

```

Input 2:

```
A = ['I', 'n', 't', 'e', 'r', 'v', 'i', 'e', 'w', 'B', 'i', 't']

```

**Example Output**

**Example Explanation**

Explanation 1:

```
All the characteristic required for password are present in given password.

```

Explanation 2:

```
The password given does not have any special character and also it does not have any numerical digit.

```

```cpp
int Solution::solve(string A) {
    if(A.length()<8 || A.length()>15){
        return 0;
    }
    int a = 0;
    string arr = "@#%&!$*";
    for(int i=0; i<A.length(); i++){
        if(isupper(A[i])){
            a += 1;
        }
        else if(islower(A[i])){
            a += 1;
        
        }
        else if(isdigit(A[i])){
            a += 1;
        }
        else if (arr.find(A[i]) != string::npos){
            a += 1;
        }
    }
    if(A.length()==a){
        return 1;
    }
    return 0;
}
```