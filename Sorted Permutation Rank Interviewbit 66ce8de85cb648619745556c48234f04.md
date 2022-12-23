# Sorted Permutation Rank | Interviewbit

Created: May 22, 2022 1:04 AM
Tags: Math
URL: https://www.interviewbit.com/problems/sorted-permutation-rank/

Given a string, find the rank of the string amongst its permutations sorted lexicographically. 
 Assume that no characters are repeated.

**Example :**

```
Input : 'acb'
Output : 2

The order permutations with letters 'a', 'c', and 'b' :
abc
acb
bac
bca
cab
cba

```

The answer might not fit in an integer, so return `your answer % 1000003`

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
int factorial(int n){
    if(n==1){
        return 1;
    }
    else{
        return n*(factorial(n-1))%1000003;
    }
}

int lexographicalrank(string A){
    int n = A.length()-1;
    int ans = 1;
    for(int i=0; i<A.size()-1; i++){
        int count = 0;
        for(int j = i+1; j<A.size(); j++){
            if(A[i]>A[j]){
                count++;
            }
        }
        ans += (count*factorial(n-i))%1000003;

    }

    return ans%1000003;
}
int Solution::findRank(string A) {
    return lexographicalrank(A);
}
```

Algorithm

Let the given string be “STRING”. In the input string, ‘S’ is the first character. There are total 6 characters and 4 of them are smaller than ‘S’. So there can be 4 * 5! smaller strings where first character is smaller than ‘S’, like followingR X X X X X I X X X X X N X X X X X G X X X X XNow let us Fix ‘S’ and find the smaller strings starting with ‘S’.

Repeat the same process for T, rank is 4*5! + 4*4! +…

Now fix T and repeat the same process for R, rank is 4*5! + 4*4! + 3*3! +…

Now fix R and repeat the same process for I, rank is 4*5! + 4*4! + 3*3! + 1*2! +…

Now fix I and repeat the same process for N, rank is 4*5! + 4*4! + 3*3! + 1*2! + 1*1! +…

Now fix N and repeat the same process for G, rank is 4*5! + 4*4! + 3*3! + 1*2! + 1*1! + 0*0!

Rank = 4*5! + 4*4! + 3*3! + 1*2! + 1*1! + 0*0! = 597

Note that the above computations find count of smaller strings. Therefore rank of given string is count of smaller strings plus 1. The final rank = 1 + 597 = 598