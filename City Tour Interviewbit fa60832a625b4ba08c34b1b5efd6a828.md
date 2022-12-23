# City Tour | Interviewbit

Created: May 22, 2022 11:46 PM
Tags: Math, Very Hard Question
URL: https://www.interviewbit.com/problems/city-tour/

**Problem Description**

There are **A** cities numbered from **1** to **A**. You have already visited **M** cities, the indices of which are given in an array **B** of **M** integers.

If a city with index **i** is visited, you can visit either the city with index **i-1** (**i** >= 2) or the city with index **i+1** (**i** < **A**) if they are not already visited. Eg: if **N** = 5 and array **M** consists of [3, 4], then in the first level of moves, you can either visit 2 or 5.

You keep visiting cities in this fashion until all the cities are not visited. Find the number of ways in which you can visit all the cities modulo **10^9+7**.

**Input Format** 
`The 1st argument given is an integer A, i.e total number of cities.
The 2nd argument given is an integer array B, where B[i] denotes ith city you already visited.`

**Output Format** 
`Return an Integer X % (1e9 + 7), number of ways in which you can visit all the cities.`
 **Constraints** 
`1 <= A <= 1000
1 <= M <= A
1 <= B[i] <= A`

**For Example**

**Input:** 
`A = 5
B = [2, 5]`
 **Output:** 
`6`
 **Explanation:** 
`All possible ways to visit remaining cities are :
1. 1 -> 3 -> 4
2. 1 -> 4 -> 3
3. 3 -> 1 -> 4
4. 3 -> 4 -> 1
5. 4 -> 1 -> 3
6. 4 -> 3 -> 1`

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
typedef long long int lint;

const lint modulo=1000000007;
const int tope=1001;

lint combi[tope][tope];
lint expo[tope];
bool flag;

void precompute() {
    if(flag) return;
    flag = 1;
    for(int n = 0; n < tope; n += 1) {
        for(int k = 0; k <= n; k += 1) {
	        if (k == 0 or k == n) {
	            combi[n][k] = 1;
	        }
	        else {
	            combi[n][k] = (combi[n-1][k] + combi[n-1][k-1]) % modulo;
	        }
        }
    }
    expo[0] = 1;
    for (int i = 1; i < tope; i += 1) {
        expo[i] = (2 * expo[i-1]) % modulo;
    }
}

int Solution::solve(int n, vector<int> &v) {
    precompute();
    int m = v.size();
    lint ans=1;
    sort(v.begin(), v.end());
    int ant = v[0]-1;
    for (int i = 1; i < m; i += 1) {
        int k = v[i] - v[i-1] - 1;
        if (k > 0) {
          lint act = expo[k-1];
          ans = ((act * ans)%modulo * combi[ant+k][k]%modulo) % modulo;
          ant += k;
        }
    }
    ans = (ans * combi[ant+n-v[m-1]][n-v[m-1]])%modulo;
    return (int)ans;
}
```