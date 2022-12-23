# Two Stores | Interviewbit

Created: May 13, 2022 5:51 PM
URL: https://www.interviewbit.com/problems/two-stores/

**Problem Description**

You want buy **A** candies, there are two candy strores in your town.
The stores sell candies in packets, first store sells **B candies for C rupees** and the other store sells **D candies for E rupees**.
Find minimum cost to **buy exactly A candies** if you can buy any amout of packets from both the stores.
If it is not possible to do so return **-1**.

**Problem Constraints**

**Input Format**

**Output Format**

**Example Input**

Input 1:

```
A = 5
B = 3
C = 3
D = 3
E = 2

```

Input 2:

```
A = 7
B = 1
C = 1
D = 3
E = 2

```

**Example Output**

**Example Explanation**

Explanation 1:

```
There no way to buy exactly 5 candies from stores.

```

Explanation 2:

```
We buy two packets from second store and 1 packet from first store.
11 + 23 = 7
11 + 22 = 5

```

Note:You only need to implement the given function. Do not read input, instead use the arguments to the function. Do not print the output, instead return values as specified. Still have a question? Checkout [Sample Codes](https://www.interviewbit.com/pages/sample_codes/) for more details.

```cpp
class Solution:
    # @param A : integer
    # @param B : integer
    # @param C : integer
    # @param D : integer
    # @param E : integer
    # @return an integer
    def solve(self, A, B, C, D, E):
        m = float('inf')
        for i in range(A//B+1):
            if(A-i*B)%D==0:
                m = min(m, C*i + ((A - B*i)//D)*E)
        if m == float('inf'):
            return -1
        else:
            return m
```