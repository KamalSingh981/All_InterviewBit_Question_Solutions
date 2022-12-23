# Atoi | Interviewbit

Created: June 17, 2022 2:25 AM
Tags: String
URL: https://www.interviewbit.com/problems/atoi/

Implement atoi to convert a string to an integer.

**Example :**

```
Input : "9 2704"
Output : 9

```

*Note: There might be multiple corner cases here. Clarify all your doubts using “See Expected Output”.*

> 
> 
> 
> **Questions:**
> 
> **Q1.** Does string contain whitespace characters before the number? **A.** Yes
> 
> **Q2.** Can the string have garbage characters after the number? **A.** Yes. Ignore it.
> 
> **Q3.** If no numeric character is found before encountering garbage characters, what should I do? **A.** Return 0.
> 
> **Q4.** What if the integer overflows? **A.** Return INT_MAX if the number is positive, INT_MIN otherwise.
> 

**Warning : DO NOT USE LIBRARY FUNCTION FOR ATOI.***If you do, we will disqualify your submission retroactively and give you penalty points.*

```cpp
int Solution::atoi(const string A) {
    int i=0;
    while(A[i]==' '){
        i++;
    }
    bool sign = 0;
    bool fal = false;
    if(A[i] == '-'){
        sign = true;
        i++;
    }
    else if(A[i] == '+'){
        i++;
    }
    long long ans = 0;
    while(A[i] >= '0' && A[i]<='9' && i<A.length())  {
        fal = true;
        ans = ans*10 + (A[i]-'0');
        if(ans>INT_MAX){
            if(sign){
                return INT_MIN;
            }
            else{
                return INT_MAX;
            }
        }
        i++;
    }
    if(fal){
        if(sign){
            return -ans;
        }
        else{
            return ans;
        }
    }
    return 0;
}
```

```cpp
int Solution::atoi(const string str) {
    if(str == "") return 0;
        stringstream ss(str);
        int ret;
        ss>>ret;
        return ret;
}
```