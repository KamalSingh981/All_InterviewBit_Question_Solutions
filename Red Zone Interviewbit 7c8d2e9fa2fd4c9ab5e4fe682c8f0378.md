# Red Zone | Interviewbit

Created: June 18, 2022 5:01 PM
Tags: Binary Search, Hard
URL: https://www.interviewbit.com/problems/red-zone/

**Problem Description**

There are many people who believe that the earth is flat and NASA is a scam. They call themselves **Flat Earthers**. They were already worried that the 6 feet social distancing rule might push some people out of the earth.

Now, they decided to think about a new issue. Since the earth is flat ( or so they think), let's imagine it as an infinite 2D grid. They have the coordinates of certain points which are **orange zones** and have some COVID-19 cases reported. Now each day the orange zones become more fatal. After **d** days, all the locations **within a euclidean distance of d** of a particular orange zone can be affected by this zone.

They know **N** orange zones, each of whose coordinates are given by **(A[i][0], A[i][1])**. Now, a location is considered a **red zone** if it is affected by at least **B** orange zones. You need to find the first day at which the first red zone is reported.

**Problem Constraints**

2 <= B <= N <= 100

0 <= A[i][0], A[i][1] <= 109

**Input Format**

The first argument contains a 2D array A of size N, denoting the coordinates of the orange zones.

The second argument contains an integer B.

**Output Format**

Return the first day at which the first red zone is reported.

**Example Input**

Input 1:

```
  A :
  [
    [8, 5]
    [0, 4]
    [3, 6]
  ]
  B : 3

```

Input 2:

```
  A :
  [
    [2, 3]
    [9, 4]
    [10, 3]
  ]
  B : 2

```

**Example Output**

Output 1:

```
  5

```

Output 2:

```
  1

```

**Example Explanation**

Explanation 1:

```
  One of the red zones will be (5, 4) and it is within a distance of 5 from all the orange zones.

```

Explanation 2:

```
  One of the red zones will be (9, 3) and it is within a distance of 1 from 2 orange zones.

```

```cpp
a = []
n, k = 0, 0
def check(r):
    c=0
    for i in range(n):
        for j in range(i+1,n):
            g = a[j]-a[i]
            d = abs(g)
            if d > 2*r: 
                continue
            mid = (a[i]+a[j])/2
            h = (r**2-(d/2)**2)**0.5
            per = complex(-g.imag,g.real)*(h/d)
            c1=c2=2
            for l in range(n):
                if l==i or l==j:
                    continue
                if abs(a[l]-(mid-per)) <= r:
                    c1 += 1
                if abs(a[l]-(mid+per)) <= r:
                    c2 += 1
            if c1 > c:
                c = c1
            if c2 > c:
                c = c2
    return c >= k

class Solution:
    # @param A : list of list of integers
    # @param B : integer
    # @return an integer
    def solve(self, A, B):
        global n,k
        n = len(A)
        a.clear()
        for i in range(n):
            a.append(complex(A[i][0],A[i][1]))
        k = B
        l=1
        h=2000000000
        while h-l>1:
            m = (l+h)>>1
            if check(m):
                h=m
            else: 
                l=m
        if check(l):
            return l
        else:
            return h
```