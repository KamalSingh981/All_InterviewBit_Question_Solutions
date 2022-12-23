# Largest Permutation | Interviewbit

Created: July 25, 2022 1:23 PM
Tags: GreedyAlgorithm
URL: https://www.interviewbit.com/problems/largest-permutation/

```cpp
vector<int> Solution::solve(vector<int> &A, int B) {
    
    for(int i = 0; i<A.size() && B>0; i++){
        int index = i;
        for(int j= i + 1 ; j<A.size(); j++){
            if(A[index] < A[j]){
                index = j;
            }
        }
        
        if(i == index){
            B++;
        }
        int temp = A[i];
        A[i] = A[index];
        A[index] = temp;
        B--;
    }
    
    return A;
}
```

**Problem Description**

Given an integer array **A** of size **N** consisting of unique integers from 1 to N. You can swap any two integers atmost **B** times.

Return the largest lexicographical value array that can be created by executing atmost B swaps.

**Problem Constraints**

**Input Format**

First argument is an integer array A of size N.

Second argument is an integer B.

**Output Format**

Return an integer array denoting the largest lexicographical value array that can be created by executing atmost B swaps.

**Example Input**

Input 1:

```
 A = [1, 2, 3, 4]
 B = 1
```

Input 2:

```
 A = [3, 2, 1]
 B = 2
```

**Example Output**

Output 1:

```
 [4, 2, 3, 1]
```

Output 2:

```
 [3, 2, 1]
```

**Example Explanation**

Explanation 1:

```
 In one swap we can swap (1, 4) so that the array becomes : [4, 2, 3, 1].
```

Explanation 2:

```
 Array is already the largest lexicographical value array.
```

![Largest%20Permutation%20Interviewbit%203ab1557c9b264865a1b8e11c48fa64f9/superman.e804d3.png](Largest%20Permutation%20Interviewbit%203ab1557c9b264865a1b8e11c48fa64f9/superman.e804d3.png)