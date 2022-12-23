# Commutable Islands | Interviewbit

Created: July 30, 2022 12:58 AM
Tags: Graphs
URL: https://www.interviewbit.com/problems/commutable-islands/

There are **A** islands and there are **M** bridges connecting them. Each bridge has some **cost** attached to it.

We need to find bridges with **minimal cost** such that all islands are connected.

It is guaranteed that input data will contain **at least one** possible scenario in which all islands are connected with each other.

**Input Format:**

```
The first argument contains an integer, A, representing the number of islands.
The second argument contains an 2-d integer matrix, B, of size M x 3:
    => Island B[i][0] and B[i][1] are connected using a bridge of cost B[i][2].

```

**Output Format:**

```
Return an integer representing the minimal cost required.

```

**Constraints:**

```
1 <= A, M <= 6e4
1 <= B[i][0], B[i][1] <= A
1 <= B[i][2] <= 1e3

```

**Examples:**

```
Input 1:
    A = 4
    B = [   [1, 2, 1]
            [2, 3, 4]
            [1, 4, 3]
            [4, 3, 2]
            [1, 3, 10]  ]

Output 1:
    6

Explanation 1:
    We can choose bridges (1, 2, 1), (1, 4, 3) and (4, 3, 2), where the total cost incurred will be (1 + 3 + 2) = 6.

Input 2:
    A = 4
    B = [   [1, 2, 1]
            [2, 3, 2]
            [3, 4, 4]
            [1, 4, 3]   ]

Output 2:
    6

Explanation 2:
    We can choose bridges (1, 2, 1), (2, 3, 2) and (1, 4, 3), where the total cost incurred will be (1 + 2 + 3) = 6.

```

```cpp
//Kruskal's Algo

int fun(int x, vector<int> &p){
    if(x==p[x]) return x;
    return p[x]=fun(p[x],p);
}

int Solution::solve(int n, vector<vector<int> > &v){
    sort(v.begin(), v.end(), [](auto &a, auto &b){
        return a[2]<b[2];
    });
    vector<int> p(n+1);
    for(int i=1; i<=n; i++) p[i]=i;
    int ans=0, i=0, c=0;
    while(c<n-1){
        int sp=fun(v[i][0], p);
        int dp=fun(v[i][1], p);
        if(sp!=dp){
            ans+=v[i][2];
            p[dp]=sp;
            c++;
        }
        i++;
    }
    return ans;
}
```