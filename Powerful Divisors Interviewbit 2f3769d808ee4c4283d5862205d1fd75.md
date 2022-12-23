# Powerful Divisors | Interviewbit

Created: May 24, 2022 2:59 PM
Tags: Math, Sieve of Eratosthenes
URL: https://www.interviewbit.com/problems/powerful-divisors/

**Problem Description**

You are given an integer array **A** of length **N**.
 For every integer **X** in the array, you have to find out the number of integers **Y**, such that **1 <= Y <= X**, and the number of divisors of Y is a power of 2.

For example, 6 has the following divisors - [1, 2, 3, 6]. This is equal to 4, which is a power of 2.
 On the other hand, 9 has the following divisors [1, 3, 9] which is 3, which is not a power of 2.

Return an array containing the answer for every X in the given array.

**Problem Constraints**

1 <= N <= 105
 1 <= Amax <= 106
 Sum of Amax over all test cases will not exceed 5 * 106

**Input Format**

**Output Format**

**Example Input**

Input 1:

```
A = [1, 4]

```

Input 2:

```
A = [5, 10]

```

**Example Output**

Output 1:

```
[1, 3]

```

Output 2:

```
[4, 8]

```

**Example Explanation**

Explanation 1:

```
The numbers 1, 2, 3 have the required number of divisors.
```

Explanation 2:

```
Only 4 and 9 are the numbers less than or equal to 10 which do not have the required number of divisors.

```

# My code

```cpp
vector < int > Solution::powerfulDivisors(vector < int > & A) {
    int a = 1;
    for (int i = 0; i < A.size(); i++) {
        a = max(a, A[i]);
    }
    int arr[a];
    fill_n (arr, a, 1);
    for(int i=2; i<=a; i++){
        int k = 1;
        for(int j=i; j<=a; j=i*k){
            k++;
            arr[j-1]++;
        }
    }
    int d = 0;
    for(int i=0; i<=a; i++){
        int count = 0;
        int temp = arr[i];
        bool flag = true;
        for(int j=0; j<32; j++){
            if(count>1){
                flag = false;
                break;
            }
            else if(temp&1 == 1){
                count++;
            }
            temp = temp>>1;
        }
        if(flag){
            d += 1;
            arr[i] = d;
        }
        else{
            arr[i] = d;
        }

    }
    vector<int> ans;
    for(int i =0; i<A.size(); i++){
        ans.push_back(arr[A[i]-1]);
    }
    return ans;
}
```

# Interview bit code

```
#define aMax 1000001
vector<int> factors(aMax,1);
void factorInit()
{

    factors[0] = 0;
    for(int i =2; i<aMax;++i)
    {
        for(int j = i; j<aMax ; j+=i)
        {
            factors[j] +=1;
        }
    }

    int count =0 , num;
    for(int i = 1; i<aMax; ++i)
    {

        num = factors[i];
        if((num&(num-1))==false) ++count;

        factors[i] = count;
    }

}
vector<int> Solution::powerfulDivisors(vector<int> &A)
{
    if(factors[0]==1)
    {
        factorInit();
    }
    vector<int> ans(A.size());

    for(int i = 0; i<A.size();++i)
    {
        ans[i] = factors[A[i]];
    }
    return ans;
}
```