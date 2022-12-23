# Sum Of Fibonacci Numbers | Interviewbit

Created: July 26, 2022 4:25 PM
Tags: GreedyAlgorithm
URL: https://www.interviewbit.com/problems/sum-of-fibonacci-numbers/

```cpp
int Solution::fibsum(int k) {
    
    int f1 = 1;
    int f2 = 1;
    vector<int> a = {1,1}; // This array contains all the fibonacci numbers smaller than or equal to k
    while(f2 <= k ){
        int next = f1 + f2;
        a.push_back(next);
        f1 = f2;
        f2 = next;
    }
    
    int n = a.size() -1;
    int ans = 0;
    while(k){  // running the loop till k is not equal to zero
        if(k>= a[n]){
            ans++;
            k = k - a[n];        
        }
        else{
            n--;
        }
    }
    return ans;    
}
```

How many minimum numbers from `fibonacci` series are required such that sum of numbers should be equal to a given Number `N`?**Note : repetition of number is allowed.**

**Example:**

```
N = 4
Fibonacci numbers : 1 1 2 3 5 .... so on
here 2 + 2 = 4
so minimum numbers will be 2

```

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.