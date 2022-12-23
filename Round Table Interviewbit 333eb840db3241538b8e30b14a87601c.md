# Round Table | Interviewbit

Created: May 10, 2022 12:48 PM
URL: https://www.interviewbit.com/problems/round-table/

**Problem Description**

There is a party at Ram's house, he will be inviting **A** friends to his party.
There is round table at his house which has **A+1 seats**.
Among all those friends Shyam is Ram's best friend and Ram wants to sit with him.
Find the number of ways to sit such that Ram and Shayam will sit together.
Since this number can be very large take modulo **109 + 7**.

**Problem Constraints**

**Input Format**

**Output Format**

**Example Input**

**Example Output**

**Example Explanation**

Explanation 1:

```
Let the two people be
1 -> Ram
2 -> Shyam
Then the possible arrangements are {1, 2}, {2, 1}
```

Explanation 2:

```
Let the three people be
1 -> Ram
2 -> Shyam
3 -> Third friend
Then the possible arrangements are {1, 2, 3}, {3, 1, 2}, {2, 1, 3}, {3, 2, 1}
```

```cpp
int Solution::solve(int A) {
    int mod = 1e9+ 7;
    long ans = 2;
    for(int i=1; i<A+1;i++){
        ans = (ans*i)%mod;
    }
    return ans;
}
```