# Permutation Swaps! | Interviewbit

Created: July 27, 2022 9:22 PM
Tags: Graphs
URL: https://www.interviewbit.com/problems/permutation-swaps/

**Problem Description**

Rishabh has a permutation **A** of **N** integers 1, 2, ... N but he doesn't like it. Rishabh wants to get a permutation **B**.

Also, Rishabh has some **M** good pairs given in a form of 2D matrix **C** of size `M x 2`  where **(C[i][0], C[i][1])** denotes that two indexes of the permutation **A**.

In one operation he can swap **Ax** and **Ay** only if **(x, y)** is a good pair.

You have to tell whether Rishabh can obtain permutation **B** by performing the above operation any number of times on permutation **A**.

If the permutation **B** can be obtained return **1** else return **0**.

**Problem Constraints**

- 2 <= N <= 10
    
    5
    
- 1 <= M <= 10
    
    5
    
- 1 <= A[i], B[i] <= N
- A[i] and B[i] are all distinct.
- 1 <= C[i][0] < C[i][1] <= N

**Input Format**

First arguement is an integer array **A** of size **N** denoting the permutation **A**.

Second arguement is an integer array **B** of size **N** denoting the permutation **B**.

Third argument is an 2D integer array **C** of size **M x 2** denoting the **M** good pairs.

**Output Format**

If the permutation **B** can be obtained return **1** else return **0**.

**Example Input**

Input 1:

```
 A = [1, 3, 2, 4]
 B = [1, 4, 2, 3]
 C = [
        [3, 4]
     ]

```

Input 2:

```
 A = [1, 3, 2, 4]
 B = [1, 4, 2, 3]
 C = [
        [2, 4]
     ]

```

**Example Output**

**Example Explanation**

Explanation 1:

```
 As A != B you have to perform operations on A but there is only good pair available i,e (3, 4) so if you swap
 A3 with A4 you get A = [1, 3, 4, 2] which is not equal to B so we will return 0.

```

Explanation 2:

```
 As A != B you have to perform operations on A but there is only good pair available i,e (2, 4) so if you swap
 A2 with A4 you get A = [1, 4, 2, 3] which is equal to B so we will return 1.

```

```cpp
int findparent(int el, vector<int> &ds){
    if(ds[el] == el) return el;
    return findparent(ds[el], ds);
}

int Solution::solve(vector<int> &A, vector<int> &B, vector<vector<int> > &C) {
    
    
    int  n = A.size();
    vector<int> ds(n+1);
    
    for(int i =0; i<= n; i++){
        ds[i] = i;
    }
    
    for(vector<int> x: C){
        int el1 = A[x[0] -1];
        int el2 = A[x[1] -1];
        
        int p1 = findparent(el1, ds);
        int p2 = findparent(el2, ds);
        
        if(p1 != p2){
            ds[p2] = p1;
        }
    }
    
    
    for(int i =0; i<n; i++){
        if(A[i] == B[i]) continue;
        else if(findparent(A[i], ds) == findparent(B[i], ds)) continue;
        else return 0;
    }
    return 1;
}
```