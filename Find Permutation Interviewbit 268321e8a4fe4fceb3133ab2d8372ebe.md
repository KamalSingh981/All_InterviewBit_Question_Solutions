# Find Permutation | Interviewbit

Created: May 15, 2022 1:36 AM
URL: https://www.interviewbit.com/problems/find-permutation/

Given a positive integer `n` and a string `s` consisting only of letters *D* or *I*, you have to find any permutation of first `n` positive integer that satisfy the given input string.

*D* means the next number is smaller, while *I* means the next number is greater.

**Notes**

- Length of given string `s` will always equal to `n - 1`
- Your solution should run in linear time and space.

**Example :**

```
Input 1:

n = 3

s = ID

Return: [1, 3, 2]

```

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
vector<int> Solution::findPerm(const string A, int B) {
    // The algorithm is:
    // if we get "D" then we will append the integer in from last of the range and subtract  from it,
    // else we will append from  1 and and added to increament it.

    vector<int> ans;
    int inc = 1, dec = B;
    for(int i = 0; i<A.size();i++){
        if(A[i]=='D'){
            ans.push_back(dec);
            dec--;
        }
        else{
            ans.push_back(inc);
            inc++;
        }
    }
    ans.push_back(inc);
    return ans;
}
```