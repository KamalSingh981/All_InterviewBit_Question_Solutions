# Diagonal Flip | Interviewbit

Created: May 9, 2022 1:48 AM
URL: https://www.interviewbit.com/problems/diagonal-flip/

**Problem Description**

Given a square **binary matrix** of drimensions **N×N**.**Flip the matrix diagonally** and return the matrix.

**Problem Constraints**

**Input Format**

**Output Format**

**Example Input**

Input 1:

```
A = 4
B = [[1, 0],
     [0, 1]]

```

Input 2:

```
A = [[1, 0],
     [1, 0]]

```

**Example Output**

Output 1:

```
[[1, 0],
 [0, 1]]
```

Output 2:

```
[[1, 1],
 [0, 0]]

```

**Example Explanation**

Explanation 1:

```
We will swap the values at positions (1, 2) and (2, 1).

```

Explanation 2:

```
We will swap the values at positions (1, 2) and (2, 1).

```

```cpp
vector<vector<int> > Solution::solve(vector<vector<int> > &A) {
    int ar = A.size();
    int ac = A[0].size(); 
    for(int i=0; i <ar; i++){
        for(int j=i+1; j<ac; j++){
            int temp = A[i][j];
            A[i][j] = A[j][i];
            A[j][i] = temp;
        }
    }
    return A;
}
```